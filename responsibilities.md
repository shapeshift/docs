# Software development lifecycle

## Requirements review and handoff

* Coordinate with @Diggy (Product) and @Tyler (Operations) first
* Identify product owner
* Identify any security considerations or blockers with @mrnerdhair
* Get a public meeting booked on the DAO calendar - use the `#request-calendar-events` channel in Discord
* Invite community contributors to kickoff meetings!
* Document technical requirements in this docs repo - create a new section

## Architecture planning and review

* Book times with @Major Hayes or @0xdef1cafe
* Spec out any groundwork PRs that should be completed internally
* Consider what is required first to unblock bounty hunters - think about the project management critical path

## Security considerations

* Book a review with @MrNerdHair for any security considerations
* Any changes to hdwallet should be *heavily* scrutinized
* Any new dependencies across *any* part of the stack should be reviewed carefully
* Any changes to the yarn.lock file in PRs must be thoroughly checked - this is the number one vector to inject malicious code
* Any third party integrations must be reviewed in terms of data privacy - we do not leak addresses, IP address, browser fingerprinting
* Any new CSP additions must be verified

## Technical breakdown

* Use the bounty template for all tickets for consistency
  * Remove the bounty section and add the `needs-engineering` label if we're completing internally
* Use the `needs product` tickets for any user facing changes/UI impacts
* Create milestones across every repo that your feature touches, name them exactly the same
	* Add all issues to that milestone
* **Provide an estimated completion date!**

## Bounties

* Add the `needs bounty` label for @0xean to post bounties - don't use the `bounty` label, 0xean will do this when it's posted
* Bounties can be reserved for community contributors
* Add a required by date (if possible)
* You can tip bounty hunters for work above and beyond (this is very common)
* Estimate how long it would take a team member, add padding, especially if something is up for grabs
	* Make sure to consider failed bounties, cycle time for PR reviews w/ requested changes
* Things can and will go wrong in development - protect timeline downside

## PR Reviews

* Ensuring issues are assigned to individuals, ensuring PRs are linked to issues, issues closed when complete
* Ensure features are flagged, and `develop` works with the flag off
* Get flags added to CI, Cypress, both preview and production environments for Fleek and Cloudflare (2 for each)
* You own the implementation of this feature, don't accept substandard work
* Review early and often - people are on different timezones.
* Don't be afraid to stop bounty hunters
* Treat `develop` as production, regressions will be reverted out.
* Use the `needs operations` tag and create a thread in #operations-publicchat to get things tested before merging

## Releases

* We release to production on Tuesdays and Thursdays - keep these in mind when getting PRs reviewed and merged
	* You are responsible if `develop` or production breaks with the flags off

## Goat/No Goat

* Coordinate with @Diggy or respective product owners for review prior to the goat meetings
* Coordinate with @Tyler and operations team to get these booked, starting several weeks out from your completion date
* Coordinate with support, marketing, product for owners of items

## Go live

* You are responsible for getting flags turned on and production redeployed in Cloudflare

## Maintenance and refactoring

* Use your discretion as to what shortcuts we can take to get a feature live
* Plan to have refactor/cleanup/abstraction work to do after features go live, don't prematurely abstract.
