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

Twice weekly, Tuesday and Thursdays @ 7PM UTC 

## Process

1. 24-36 hours before the scheduled release review each of the following repositories for changes since the last release.
    1. Web or its dependencies (lib, etc)
    1. Foxfarm
    1. Unchained
2. For each repository with changes create a release branch from the current develop branch. This branch should be named in the following format with XX.YY representing the major and minor versions `releases/vXX.YY.ZZ`.
3. Build the ephemeral environment for testing:
    1. For the web codebase, this can be executed with this command: `web/scripts/release.sh release vXX.YY.ZZ`
    For other codebases, run manually with these commands:
    1. go to repo directory
    1. `git fetch`
    1. `git checkout develop`
    1. `git reset --hard origin/develop`
    1. `git checkout -b releases/vXX.YY.ZZ`
    1. `git push origin releases/vXX.YY.ZZ`
4. Get the URL of the ephemeral environment created (can be found in GitHub or on CloudFlare)
5. Create a thread in the `#operations-publicchat` Discord channel with the following format. `YYYY-MM-DD repo-name releases/vXX.YY.ZZ`. For example `2022-01-18 web releases/v1.55.21`
6. In the thread create a summary of the release including new customer facing functionality or bug fixes that can help product and operations to verify functionality, ping the following workstreams by mentioning them in the discord thread and identify each of the people filling the above Roles by discord handle. Also include the URL of the ephemeral environment found in the step above. Please also alert any engineer with code shipping to production in the channel.
    1. Operations
    1. Engineering
    1. Product
7. If blocking issues are discovered in the release branch, it should be reported in the thread created above.
8. The person who has found the issue should add it to GitHub and comment on the Pull Request with a link to the issue. This will serve as the release checklist to inform the go / no-go decision on the final merge to production.
9. The Release Manager will be responsible for coordinating any fixes. If they are able to resolve the issue themselves they may, or if not they will pull in the needed engineering resources to do so. Ultimately, they may also decide to push back the release until the next window if the issues are too severe or risky given the time frame.
10. Blocking issue fixes should be merged directly into the `releases/vXX.YY.ZZ` branch.
11. Once all blocking issues have been resolved and merged into the release branch, and Operations Lead and Product Lead have signed off, the Release Manager will merge the branch to main, without doing a squash merge.
12. This needs to be done at the command line (directions to run via script also provided):

    # After testing, merge to main

    For the web codebase, you can use this script: web/scripts/release.sh main vXX.YY.ZZ
    For other codebases, these are the commands:
    1. `git checkout main`
    2. `git reset --hard origin/main`
    3. `git merge --no-ff releases/vXX.YY.ZZ`
    4. `git tag -a -m "vXX.YY.ZZ" vXX.YY.ZZ`
    5. `git push origin main --tags`

    # Delete the release branch

    For web codebase, this is also executed with the above command (the After testing command)
    For other codebases, these are the commands:
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

Shapeshift DAO will have four distinct environments that are a part of the testing and release flow: 1) development 2) release branch 3) alpha and 4) production. LaunchDarkly, pending a security review, will be used to control feature flags in all sub-production environments.

1. **Development** - This deployment will track the develop branch of the web repository. Feature flags can be controlled via LaunchDarkly.
1. **Release** - This deployment will track the latest release branch that has been created by the Release Manager. Feature flags can be controlled via LaunchDarkly for Alpha testing but once moved to production, LaunchDarkly will no longer be able to be used. 
1. **Alpha** - The environment served at `alpha.shapeshift.com`. This build will be identical to the production build and deployed alongside with production. The only difference between the two will be the ability to use LaunchDarkly for feature flagging.
1. **Production** - The environment served at `app.shapeshift.com`. Identical to the Alpha build, but with no ability to control feature flags via LaunchDarkly.
