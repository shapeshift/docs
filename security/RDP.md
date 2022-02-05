
# ShapeShift DAO Responsible Disclosure Program

At ShapeShift, we take security seriously.

The ShapeShift DAO is happy to announce its Responsible Disclosure Program (RDP), which is designed to incentivize security researchers to actively test our products and report any vulnerabilities discovered in a manner which allows us a window of opportunity to assess and remediate the underlying issues in advance of public disclosure.

## Reporting Issues

You may report issues by sending an email to [security@shapeshift.io](mailto:security@shapeshift.io), or by opening a ZenDesk ticket via our [web form](https://shapeshift.zendesk.com/hc/en-us/requests/new?ticket_form_id=4419512276365). The ShapeShift DAO's Security Workstream will review your reports, and get back to you within 24 hours.

You can encrypt your report to the Security Workstream's [GPG key](https://ipfs.io/ipfs/bafybeicenclfzbrc3rnuknzzhiqyqzql2ax77s6oifj3hy2wolhfclv5jm/0CCAE62C4CE9AD1F.asc) if you'd like. (Previously, ShapeShift US operated a different RDP program using a [different](https://ipfs.io/ipfs/bafybeigmy2k65gxpl5u2wp56pdkr4xjkepgy2lw7ywxxsvfm6xdptl6mhu/04B97C31DF76FA40.asc) root key; [here](https://ipfs.io/ipfs/bafybeicvowvsgzb3qqxylre2diuusmao3bu5cinru7htv2htmoq5ims2a4) you can find a message signed under an [intermediate](https://ipfs.io/ipfs/bafybeieo5z3kgogurjaughcr7zssxxcrjsuzgp6kqt4hkvrnvssn24iepy/86ED7AD1A2204998.asc) ShapeShift US key which describes the program transition and confirms the new key's provenance.)


## Disclosure Policy

We ask that you keep any issues confidential for a period of 90 days following your report to us, or until they are remediated, whichever is shorter. This is intended to allow us a window of opportunity to assess and remediate the underlying issues in advance of their public disclosure. Your participation in this program is contingent on this confidentiality; you may choose to disclose whatever you wish at any time, but doing so during the confidentiality period will forfeit any rewards you may have otherwise been eligible for.

## Researcher Guidelines

All software the DAO maintains is open-source and available to the public, and you do not need special permission from us to perform security research on our software or systems. Rest assured that whether or not you choose to participate in our Responsible Disclosure Program, we will not pursue any legal action against you or your company for unlawful access of computer systems, access of confidential information, or damages to our systems. Still, we request that you follow Wheaton's Law and conduct your research in a manner respectful of us and our users.

- Please refrain from attempting to cause denials of service by leveraging high volumes of traffic.
- Please don't use any vulnerabilities you may find against any of our users if you don't have their permission.
- Please avoid intentionally degrading our users' experience.

When in doubt, we do have some testing environments that may come in handy if you'd like to try stuff like this. Feel free to drop into our [Discord server](https://discord.gg/shapeshift) and chat with us in that case; we'll work with you.

### Submitting Patches

Since all the code eligible covered by the RDP is open-source, you may also want to contribute a patch for the issues you report; doing so may make you eligible for a bounty from our Engineering Workstream on top of your RDP rewards! However, please do note that submitting patches or pull requests via our ordinary engineering workflow (by definition) makes them public, which may breach the confidentiality requirement for receiving an RDP award. If you'd like to submit a patch for an issue you're reporting under the RDP, please make sure that you let us know first so that we can coordinate the process.

### Program Scope

Not everything with the word "ShapeShift" on the tin is something the ShapeShift DAO maintains. For the avoidance of confusion, this program has a specifically defined scope; anything listed below is covered, anything that's not isn't.

- Any smart contract code developed by the DAO
- Any smart contract code deployed by the DAO on-chain on a mainnet (i.e. L2s are in-scope, but not testnets)
- The specific projects hosted at the following GitHub repositories:
  -  [shapeshift/web](https://github.com/shapeshift/web)
  -  [shapeshift/lib](https://github.com/shapeshift/lib)
  -  [shapeshift/unchained](https://github.com/shapeshift/unchained)
  -  [shapeshift/hdwallet](https://github.com/shapeshift/hdwallet)
  -  [keepkey/keepkey-firmware](https://github.com/keepkey/keepkey-firmware)
- Any software hosted under the [ShapeShift](https://github.com/shapeshift/) or [KeepKey](https://github.com/keepkey/) GitHub Orgs, or the [@shapeshiftoss](https://www.npmjs.com/org/shapeshiftoss) NPM org, *if it's a dependency of something else in-scope*
  - Examples of dependencies that are in-scope:
    -  [shapeshift/fiojs](https://github.com/shapeshift/fiojs)
    -  [keepkey/python-keepkey](https://github.com/keepkey/python-keepkey)
    -  [keepkey/device-protocol](https://github.com/keepkey/device-protocol)
  - Examples of things that are hosted in these locations, but aren't dependencies of something in-scope:
    -  [shapeshift/cluster-launcher](https://github.com/shapeshift/cluster-launcher)
    -  [shapeshift/foxfarm](https://github.com/shapeshift/foxfarm)

The DAO's RDP covers code, not specific running instances of that code, but it's often helpful to think in those terms when planning your targets. Here's a handy (though not exhaustive!) cheat-sheet:

- In-scope
  -  [app.shapeshift.com](https://app.shapeshift.com) (runs [shapeshift/web](https://github.com/shapeshift/web))
  -  [api.bitcoin.shapeshift.com](https://api.bitcoin.shapeshift.com) (runs [shapeshift/unchained](https://github.com/shapeshift/unchained))
  -  [api.ethereum.shapeshift.com](https://api.ethereum.shapeshift.com) (runs [shapeshift/unchained](https://github.com/shapeshift/unchained))
  - Physical (or emulated!) KeepKey devices
- Out-of-scope
  -  [shapeshift.com](https://shapeshift.com) (hosted by WebFlow, a third-party)
  -  [shapeshift.zendesk.com](https://shapeshift.zendesk.com) (hosted by ZenDesk, a third-party)
  -  [shapeshift-io.hellonext.co](https://shapeshift-io.hellonext.co/) (hosted by HelloNext, a third-party)
  -  [beta.shapeshift.com](https://beta.shapeshift.com) (a legacy system maintained by the ShapeShift Foundation, not the ShapeShift DAO)
  -  [auth.shapeshift.com](https://auth.shapeshift.com) (a legacy system maintained by the ShapeShift Foundation, not the ShapeShift DAO)
  -  [portal.shapeshift.io](https://portal.shapeshift.io) (a legacy system maintained by the ShapeShift Foundation, not the ShapeShift DAO)
  -  The ShapeShift [mobile app](https://apps.apple.com/us/app/shapeshift-buy-trade-crypto/id996569075) (a legacy system maintained by the ShapeShift Foundation, not the ShapeShift DAO)
  -  [portis.io](https://portis.io) (Portis is now a separate company)
  -  [coincap.io](https://coincap.io) (CoinCap is now a separate company)

If you find an issue with something that isn't in scope, please still make a report; we'll do our best to make sure they're routed to the right people and handled appropriately. However, we can't offer any rewards for reports about out-of-scope systems, and we can't make any guarantees about the resolution of issues in systems the DAO doesn't maintain.

### Valid Issues

Any valid, in-scope issues is covered under this program; however, what exactly "valid" means is at our sole discretion, and if you report an issue which we don't consider valid you will not receive a reward for that issue. To help set expectations, here's a few things that we don't consider valid:

- Disclosure of API keys that aren't supposed to be kept secret
- Clickjacking attacks against sites that don't maintain user login sessions
- TLS settings which don't quite match someone-or-other's particular recommendations
- Open S3 buckets which don't have any confidential information in them
- Most non-critical findings from automated vulnerability scanners
- Most `Host` header injections (the ability to attack yourself isn't a security issue)
- Information disclosure issues that only disclose publicly available information (like stuff that's recorded on a blockchain)
- Attacks which require physical access to a user's device (including KeepKey, which is not intended to be tamper-resistant)
- Attacks which require arbitrary code execution on a user's computer (except KeepKey, where protecting against that sort of thing is the whole point)

This list is not exhaustive, and we'll update it with more salient examples as we discover points of confusion; still, hopefully it's relatively self-explanatory.

Whether an issue is valid usually boils down to one of threat model; if you'd like to discuss the threat model we use for the various in-scope projects, or get clarification about the status of a particular issue, feel free to drop into our [Discord](https://discord.gg/shapeshift) server and have a chat with our security team.

## Rewards

We offer two types of reward for your reports under this program: a Goodwill Bounty and an Additional Bounty. Goodwill Bounties are $200 (in xDAI) and are awarded to every report of a valid issue under this program as long as you follow the program guidelines and respect our 90-day confidentiality period. Additional Bounties are recommended to the ShapeShift DAO by its Bounty Committee, which meets on a periodic basis to assess the impact of resolved RDP reports and consider Additional Bounty awards.

The Bounty Committee's recommendations are made entirely at its own discretion, and the payment of them is made entirely at the discretion of the DAO itself. Not every issue will receive an Additional Bounty award; low-impact issues may receive only the Goodwill Bounty. However, this process means that there is no fixed budget or upper limit for bounty awards; each award is made via a formal DAO governance proposal, which can draw on all the resources of the DAO. (Among other benefits, this process means that RDP bounties are not subject to the vagaries of the budget cycle; for example, if you report a high-impact vulnerability, your award will not be reduced because someone else reported something else serious before you and drained the budget.)

### Hall of Fame NFT

Upon your report of a valid, in-scope issue, you will be issued a ShapeShift Hall of Fame NFT. Your Hall of Fame NFT represents both our recognition of your contribution and your interest in any associated Additional Bounty. It's our hope that these NFTs will be of value to you as a researcher, providing assured public recognition and an overall smoother bounty-hunting experience.

For the duration of the confidentiality period, your NFT will be locked. It will not be tradable, and will be subject to revocation if your report is determined not to be of a valid issue or if the issue you've reported is disclosed publicly. However, once the confidentiality period expires, your NFT will be unlocked and updated with a description of the issue you reported.

When your NFT is unlocked you will receive your Goodwill Bounty, and you may also update the NFT to contain a name and hyperlink of your choice. (These submissions must be professional, and are subject to content moderation at the sole discretion of the DAO and its Security Workstream.) This will provide public, verifiable recognition of your contribution, which we hope will be of value in your professional career.

We take care when evaluating reports for award of an Additional Bounty; the process will take at least two weeks after your issue is resolved, and could take as long as several months. We recognize, though, that you may not want to wait, and our policy of paying Additional Bounties to NFT holders means that you don't have to; instead, you can sell your NFT. Hall of Fame NFT buyers purchase the rights to any Additional Bounty which may be forthcoming, but they also purchase the risk associated with the wait and the uncertainty associated with the award process. A specific goal of the RDP is for Hall of Fame NFTs to attract buyers who are not simply collectors or speculators, but who have both experience with our process and a good understanding of the impact of security issues and can give you a fair price, allowing us to retain our high process quality standards for making bounty awards without compromising your options as a researcher.
