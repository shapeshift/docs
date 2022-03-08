# ShapeShift DAO Engineering Workstream: Technical Integration Process

#### Background:

The engineering workstream is responsible for the long term development, delivery and maintenance of technical products required for the Shapeshift DAO to reach its vision of becoming an open-source, multi-chain, self-custody crypto platform enabling billions to achieve financial sovereignty. Our ability to effectively integrate and interface with contributions from teams, open-source contributors and other DAOs will be critical to our success as a workstream and as a DAO.

#### Purpose

This document will act as a starting point to guide your team’s interaction with the engineering workstream. Your team’s success is of great importance to the workstream, and we hope that this process will help to ensure our mutual goals are realized. We aim to align our teams on the high level architectural path, engineering standards around code quality and any ongoing operational requirements. We believe that by outlining our requirements early in the process, approving designs and setting up points of contact we can avoid wasted efforts further down the road for both of our teams.

#### Scope

This process is intended to be followed for large technical initiatives and not meant to be followed for small bounties that are typically resolvable in a single Pull Request. While large is a relative word, our goal is for projects that are spanning several weeks to months to follow this process. If you are unsure if you need to follow this process, please reach out to the engineering workstream directly, and we can assist with the determination.

#### Process

1. Please start by familiarizing your team with the existing ShapeShift OSS Application available and its [codebase](https://github.com/shapeshift).
2. Read this document to completion, we welcome any questions on items that are not clear or ways we can improve this process.
3. Identify all the ShapeShift owned repositories that your feature will need to modify or extend, please read all documentation in those associated repositories.
4. Obtain an approved design document. Integrating teams should create a design document for their planned feature. Previous examples of these documents can be found [here](designs.md). Your document should start out as a Google document that can be used for questions and comments. Once you believe the document is completed, please reach out to @joshf on Discord to schedule a design review meeting. The first half of the meeting will be spent with core engineers individually reading your design document (in silence). The second half of the meeting will be a discussion of questions, comments or any points that need additional clarification or changes. A determination will be made from the core workstream of either approval to move forward or clear next steps to obtain that approval. Once your document is approved, please open a PR to add it to our [docs repo](https://github.com/shapeshift/docs).
    1. Specific Items that must be included in your document:
        1. List of all repositories you plan to make modifications in
        1. Any new hardware / nodes that will be required or the scaling of existing hardware
        1. Any new dependencies or third-party libraries that your feature will require
        1. Target dates for dev completion and product launch
5. Any feature or integration requiring a new contract to be deployed on chain, will require an external audit to be obtained from a reputable firm, and all comments addressed prior, at the integrator's expense.
6. Any new dependencies, cross-origin requests, integrations with centralized third parties, or modifications to code that impacts security (e.g. wallets) may require input and review from the Security Workstream.
7. Begin work on your new feature. It is recommended that you create a new branch that will act as your development branch and that you keep up to date with our development branch(es) frequently to avoid messy conflicts. We are happy to provide intermediate code reviews and welcome any changes to our documentation as your team progresses. Additionally, we will coordinate if multiple external teams are working on the same area of the code to avoid a scenario where multiple external branches may be in conflict.
8. As you near dev completion of your feature, please do the following:
    1. Notify Operations and Product workstreams.
    1. Open any remaining Pull Requests and notify the Engineering workstream via Discord to schedule a final review meeting.
    1. Keep your branch regularly updated with `develop` to avoid merge conflicts.
9. During the final review meeting, please present your feature to the engineering workstream, explain any operational concerns on the deployment, launch, and ongoing maintenance of the feature. Identify any risks with the launch and share any resources the team may need as they take ownership of the feature after the warranty period.
10. Fulfill your obligations for the 30-day warranty period, this may include on-call support if your feature demands it.
11. Provide feedback to our team and DAO on this process and how we can improve it. 

#### General requirements for acceptance

1. Code must meet our minimum standards outlined [here](standards.md). Specific languages or technologies may have additional requirements, see [here](standards.md) for a breakdown of these.
2. Integrating teams must provide a 30-day operational warranty for any new feature launch. This means that the integrating team will be responsible to mitigate, root cause and fix any production issues that arise as a result of the newly released code for a 30-day period.
