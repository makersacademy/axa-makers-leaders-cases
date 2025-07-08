# Phoenix Mutual – The Friction Factory

Phoenix Mutual is a mid-sized UK-based insurance provider with approximately 1,200 employees. Its core business includes life insurance, income protection, and retirement products. The company operates under the regulatory oversight of the Financial Conduct Authority (FCA) and must comply with the Senior Managers and Certification Regime (SM&CR), which demands clear accountability for operational risks and changes.

Historically, Phoenix ran on legacy, on-premises systems with a strict ITIL-based change management process. Releases were quarterly, approvals were layered, and most changes were coordinated via email chains and spreadsheets.

### The Modernisation Push

In the past 18 months, Phoenix has undertaken a major digital transformation:

- Infrastructure: Migrated most systems to Microsoft Azure, with Kubernetes handling service orchestration
- Development Practice: Adopted DevOps principles, encouraging continuous delivery and cross-functional teams
- Team Structure: Engineers now work in “you build it, you run it” teams, owning the entire lifecycle from code to production
- Tooling: CI/CD pipelines are built with GitHub Actions, and deployment is automated to staging, with a manual step to production
- Change Tracking: All changes are linked to Jira tickets and logged in ServiceNow, the company’s internal ITSM tool

Despite these modern workflows, engineers are frustrated. They say getting anything live is painful and slow, especially for small, routine updates.

### Act 1 – What’s Slowing Things Down and Why?

Phoenix’s delivery process remains slow, even for minor changes. Every deployment, no matter how small, requires a Jira ticket, a ServiceNow Change Record, and approval at a weekly Change Advisory Board (CAB) meeting.

Most technical steps in the delivery flow are automated. CI/CD pipelines handle testing and deployment to staging. Manual promotion is still required for production, even for standard changes. For significant changes, additional architecture and security reviews are required before CAB review.

In practice, engineers feel blocked by process. In emergency situations, they sometimes deploy changes quickly and backfill documentation later to reflect what should have happened. This has led to growing frustration among teams. They’re asking:
“If we’re deploying through tested, traceable pipelines and following good practices, why do we still need a CAB?”


### Act 2 – Is Pairing Enough?

One team suggests a way to streamline.
If two engineers pair on a change, write automated tests, and deploy through the pipeline, they believe the team should be allowed to skip both the pull request review and the CAB approval.

Their view is that pairing provides real-time review and shared accountability, and the pipeline ensures the change is traceable. The idea is not to remove control entirely, but to replace slow, external checks with something more integrated into how the team actually works.

This proposal has sparked internal debate. It raises deeper questions about what counts as a sufficient control and how confidence in safety and auditability can be preserved.


### Act 3 – Who Gets to Say It’s Safe?

Currently, Phoenix’s security lead signs off dozens of changes every week. Many are approved without in-depth code inspection. The security lead is highly trusted, but also removed from the actual implementation work.

As engineers push for more autonomy, it is unclear who should be empowered to make final deployment decisions. Teams want responsibility, but leadership is wary of losing oversight. There is no clear framework for delegated authority or how to demonstrate that a delegated decision was made responsibly.

The conversation now is not just about process. It is about trust, risk ownership, and clarity in a regulated environment.


### Act 4 – Is the Control Still Working?

Six months ago, Phoenix introduced a rule: all significant changes must include evidence of a threat model review. Initially, this sparked meaningful discussion and deeper security awareness within teams.

Today, the rule still exists, but its impact has faded. Most teams now include a generic Confluence link as “evidence” to meet the requirement. No one is actively challenging or validating the quality of the review. The control has drifted into box-ticking.

This has raised a deeper question.
Even when controls are well designed at the outset, how do you know they’re still delivering value? Who owns the responsibility to check?
