# Shapeshift DAO Release Process

## Purpose

The purpose of this document is to outline a process that standardizes a mechanism for the DAO to release code to production frequently and with checks in place to ensure the quality of those releases. We expect this process to change as we learn more and grow in our proficiencies as a DAO in releasing software. Our ultimate vision is to move towards full CI/CD with more automated testing and less manual validation.

## Roles

1. Release Manager (a CODEOWNER from the Engineering Workstream)
    1. Responsible for the end-to-end release process overall. See process below.
1. Operations Lead (someone from the Operations Workstream)
    1. Responsible for testing and confirming that expected fixes are as intended. The Operations Lead is more focused on testing defects that have been mitigated rather than new features. Assists with general regression testing.

## Cadence

Monday-Thursday @ ~6PM UTC.

## Reference

* https://release.shapeshift.com - the release environment to test against
* Click the yellow dot or green tick on the topmost commit row.
  * https://github.com/shapeshift/web/commits/release
    * Once the `fleek/build - Preview ready` check has a green tick the release is ready to test. Follow the same process when any fixes are merged to the release branch to know when the fix is ready to test.
  * https://github.com/shapeshift/web/commits/main
    * Once the `fleek/build - Preview ready` check has a green tick the release is live in production.

## Process

1. A CODEOWNER from the Engineering Workstream must run the command `yarn release` and follow the prompts to update the `release` branch.
2. Create a thread in the `#operations-publicchat` Discord channel with the following format. Use the `+` button on the left of the text input box to create a thread before pasting this template.

    Title: `release vX.Y.Z`. For example `release v1.2.3`

    Body:
    ```
    @W-Operations @W-Engineering @W-Marketing

    Owners

    * Engineering - @ (the responsible person from each team)
    * Operations - @

    Release branch

    * https://release.shapeshift.com
    * https://github.com/shapeshift/web/commits/release - to check on status of release branch.
    * https://github.com/shapeshift/web/commits/main - to check on status of production deployment.

    User facing changes

    * paste an operations-friendly summary of user facing changes in the release

    Possible regressions/risk

    * a summary of specific regression testing required based on non-user facing changes in the branch
    ```

7. Operations should be testing the release branch with the default feature flags settings, i.e. what is going into production.
8. If a new feature behind a flag is scheduled for release that day

    a. The release manager should ping someone with access to Fleek (`@0xdef1cafe` `@Apotheosis` `@gomes` `@kevin`) and ensure the respective feature flags are added to all environments. Please note there are multiple environments:
      * `develop`
      * `release`
      * `app`
      * `private`

    b. Operations should test with that flag on.
9. If blocking issues are discovered in the release branch, it should be reported in the thread created above.
10. The person who has found the issue should add it to GitHub and comment on the Pull Request with a link to the issue. This will serve as the release checklist to inform the go / no-go decision on the final merge to production.
11. The Release Manager will be responsible for coordinating any fixes. If they are able to resolve the issue themselves they may, or if not they will pull in the needed engineering resources to do so. Ultimately, they may also decide to push back the release until the next window if the issues are too severe or risky given the time frame.
12. Blocking issue fixes should be merged directly into the `release` branch.
13. Once all blocking issues have been resolved and merged into the release branch, and Operations Lead has signed off, the Release Manager should run `yarn release` again to merge the release branch into `main`.
14. This needs to be done at the command line (directions to run via script also provided):

    ## After testing, merge to main

    ### `web` repo

    The CODEOWNER can be sure that the code in the release branch does not require reviewing, as all PRs into `develop` or `release` are subject to branch proteciton and have already been reviewed by a CODEOWNER, and the release branch has been functionally tested by the operations team. This is merely an administrative task, required to be done by a CODEOWNER due to branch protection on `develop` and `main`.

    Run the `yarn release` command and follow the prompts. The script will

    1. Detect the current state of the repo (release in progress or not)
    2. Prompt you with commits that will be merged from `release` into `main`
    3. Merge `release` into `main` and push
    4. Checkout and pull `develop`
    5. Merge `main` back into `develop` and push

    ### Other repos

    1. `git checkout main`
    2. `git merge --no-ff releases/vXX.YY.ZZ`
    3. `git tag -a -m "vXX.YY.ZZ" vXX.YY.ZZ`
    4. `git push origin main --tags`

    ## Delete the release branch

    ### `web` repo

    This is also executed with the release script - you do not have to manually delete the branch.

    ### Other repos

    1. `git branch -d releases/vXX.YY.ZZ`
    2. `git push origin --delete releases/vXX.YY.ZZ`
    3. (script will soon be added to do these steps)

14. Release Manager will monitor the deployment. Once the deployment has been completed they will notify the release Discord thread for final confirmation from Operations once in production.
15. Operations Lead monitors customer channels and any applicable performance metrics / smoke tests over the next 24 hours and alerts the Release manager if any issues arise that are suspected to be from the release.
16. Our default response is to roll back if the release is expected to have broken any critical functionality. To rollback, you can find the previous release on the main branch in CloudFlare pages, click the `view build` link on the right. Then, in the upper right, you'll see a `Manage Deployment` dropdown. Choose the `Rollback` option. The deployment occurs almost immediately.

## Hotfixes

1. Hotfixes can be made out of band from our scheduled releases as dictated by the severity of the issue being mitigated.
1. We still recommend following steps 3 - 9 above in these cases. With a hotfix branch being cut from main and then merged back into main and develop once completed.

## Feature Releases in Web:

Shapeshift DAO will have four distinct environments that are a part of the testing and release flow: 1) development 2) release 3) private and 4) production. We use a hand rolled feature flagging service with no external dependencies. It can be accessed in the web app by pressing `Option + Shift + F` on macOS or `Alt + Shift + F` on Windows/Linux.

1. **Development** - This deployment will track the `develop` branch of the web repository. Feature flags can be controlled via the flags menu.
1. **Release** - This deployment will track the latest `release` branch that has been created by the Release Manager. Feature flags can be controlled via the flags menu.
1. **Private** - Serve a privacy preserving version of ShapeShift at `private.shapeshift.com`. This build will be identical to the production build and deployed alongside with production, with potentially some unstable flags enabled, and opt in user tracking for product metrics and analysis via Pendo.
1. **Production** - The production environment served at `app.shapeshift.com`.
