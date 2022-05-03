# Shapeshift DAO Release Process

## Purpose

The purpose of this document is to outline a process that standardizes a mechanism for the DAO to release code to production frequently and with checks in place to ensure the quality of those releases. We expect this process to change as we learn more and grow in our proficiencies as a DAO in releasing software. Our ultimate vision is to move towards full CI/CD with more automated testing and less manual validation.

## Roles

1. Release Manager (a code owner from the Engineering Workstream)
    1. Responsible for the end-to-end release process overall. See process below.
1. Product Lead (someone from the Product workstream)
    1. Responsible for testing of any new features or feature flags that have been enabled for this release. Will work closely with the release manager to determine if the release candidate will move to production.
1. Operations Lead (someone from the Operations Workstream)
    1. Responsible for testing and confirming that expected fixes are as intended. The Operations Lead is more focused on testing defects that have been mitigated rather than new features, but will work with Product Lead as needed on new features. Assists with general regression testing.

## Cadence

Twice weekly, Tuesday and Thursdays @ 7PM UTC.

## Process

1. On the morning of the scheduled release, review the `web` repository for changes since the last release. Any member of the ShapeShift org can create a release branch, however a CODEOWNER is required to merge it.
2. Ensure you have the [`gh` CLI tools installed](https://github.com/cli/cli#installation) to automatically create the PR.
3. Once the github cli is installed on your machine, run `gh auth login` to login to your github account through the cli. You can confirm you are logged in by running `gh auth status`.
4. Run the following commands.
    a. `git fetch --tags && git tag` - look for the most recently tagged version deployed to `main` (production).
    b. Determine the new release number based on semantic versioning. For most releases this is a patch version. For new features use a minor version. E.g. `1.3.0` goes to `1.3.1` or `1.4.0` for a patch or minor version bump respectively. To determine the semantic version type, you can preview the list of commits that will be cut for the release by running `git fetch origin && git log --oneline --first-parent origin/main..origin/develop`
    c. Run the command `yarn create-release vX.Y.Z` with your new version.
5. The previous step will automatically open a pull request in the web repository with your release branch. Wait for CI to finish the Cloudflare Pages check. Get the URL of the ephemeral environment created by finding the newly created pull request in the web repo, clicking the `Details` link at the right of the Cloudflare Pages CI check, and copying the preview URL listed in the deployment summary.
6. Create a thread in the `#operations-publicchat` Discord channel with the following format. Use the `+` button on the left of the text input box to create a thread before pasting this template.

    Title: `release vX.Y.Z`. For example `release v1.2.3`

    Body:
    ```
    @W-Operations @W-Products @W-Engineering

    release vX.Y.Z

    Owners:

    * Engineering - @ (the responsible person from each team)
    * Operations - @
    * Product - @

    Release branch

    * link to release branch on GitHub
    * link to CloudFlare preview environment to be tested against

    User facing changes

    * paste an operations-friendly summary of user facing changes in the release

    Possible regressions/risk

    * a summary of specific regression testing required based on non-user facing changes in the branch
    ```

7. Operations should be testing the release branch with the default feature flags settings, i.e. what is going into production.
8. If a new feature behind a flag is scheduled for release that day
    a. The release manager should ping someone with access to Fleek and CloudFlare (`@Major Hayes` or `@0xdef1cafe`) and ensure the respective feature flags are added to all environments. Please note there are preview and production environments building off the `develop` and `main` branches respectively in both Fleek and CloudFlare - ensure the environment variables are added to both and correctly aligned.
    b. Operations should test with that flag on.
9. If blocking issues are discovered in the release branch, it should be reported in the thread created above.
10. The person who has found the issue should add it to GitHub and comment on the Pull Request with a link to the issue. This will serve as the release checklist to inform the go / no-go decision on the final merge to production.
11. The Release Manager will be responsible for coordinating any fixes. If they are able to resolve the issue themselves they may, or if not they will pull in the needed engineering resources to do so. Ultimately, they may also decide to push back the release until the next window if the issues are too severe or risky given the time frame.
12. Blocking issue fixes should be merged directly into the `releases/vX.Y.Z` branch.
13. Once all blocking issues have been resolved and merged into the release branch, and Operations Lead and Product Lead have signed off, the Release Manager should ping a CODEOWNER to merge the release branch into `main`.
14. This needs to be done at the command line (directions to run via script also provided):

    ## After testing, merge to main

    ### `web` repo

    The CODEOWNER can be sure that the code in the release branch does not require reviewing, as all PRs into `develop` or directly into the release branch have had a CODEOWNER approval, and the release branch has been functionally tested by the operations team. This is merely an administrative task, required to be done by a CODEOWNER due to branch protection on `develop` and `main`.

    1. `yarn merge-release v1.2.3` - this will merge the release into main, push it to origin, close the release PR, and leave you on a detached head.
    2. `git checkout main`
    3. `git pull` - ensuring we have the latest upstream of `main`.
        `git log --graph --decorate --all` - sanity check to ensure the merge looks correct.
    4. `git checkout develop`
    5. `git pull` - ensuring we have the latest upstream of `develop`.
    6. `git merge main` - back merge `main` into `develop`.
        `git log --graph --decorate --all` - sanity check to ensure the merge looks correct.
    7. `git push` - push directly to develop.

    If something is wrong with the merges and you haven't pushed, reset your repo locally. If you have pushed, coordinate with another CODEOWNER to rectify the upstream repo state before force pushing anything. If we need to roll back a production release, this can be done in CloudFlare GUI.

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

14. Release Manager will monitor the deployment. Once the deployment has been completed they will notify the release Discord thread for final confirmation from Product and Operations once in production.
15. Operations Lead monitors customer channels and any applicable performance metrics / smoke tests over the next 24 hours and alerts the Release manager if any issues arise that are suspected to be from the release.
16. Our default response is to roll back if the release is expected to have broken any critical functionality. To rollback, you can find the previous release on the main branch in CloudFlare pages, click the `view build` link on the right. Then, in the upper right, you'll see a `Manage Deployment` dropdown. Choose the `Rollback` option. The deployment occurs almost immediately.

## Hotfixes

1. Hotfixes can be made out of band from our scheduled releases as dictated by the severity of the issue being mitigated.
1. We still recommend following steps 3 - 9 above in these cases. With a hotfix branch being cut from main and then merged back into main and develop once completed.

## Feature Releases in Web:

Shapeshift DAO will have four distinct environments that are a part of the testing and release flow: 1) development 2) release branch 3) alpha and 4) production. We use a hand rolled feature flagging service with no external dependencies. It can be accessed in the web app by pressing `Option + Shift + F` on macOS or `Alt + Shift + F` on Windows/Linux.

1. **Development** - This deployment will track the develop branch of the web repository. Feature flags can be controlled via the flags menu.
1. **Release** - This deployment will track the latest release branch that has been created by the Release Manager. Feature flags can be controlled via the flags menu.
1. **Alpha** - Does not currently exist, but will be served in the future at `alpha.shapeshift.com`. This build will be identical to the production build and deployed alongside with production, with potentially some unstable flags enabled, and opt in user tracking for product metrics and analysis via Pendo.
1. **Production** - The environment served at `app.shapeshift.com`. Identical to the Alpha build, but with only stable flags enabled.
