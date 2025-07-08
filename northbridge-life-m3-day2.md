# Northbridge Life - Pricing Platform Change Delivery

### Organisational Context

Northbridge Life is a large UK life and protection insurance company with more than 6,000 employees and over £40 billion in assets under management. The company operates multiple business lines, including personal life insurance, group schemes, critical illness cover, and funeral plans.

Over the past three years, Northbridge has been investing in modernising its technology estate. A major programme is underway to rebuild pricing and underwriting services as modular APIs - replacing a complex web of mainframe rulesets, Excel models, and hard-coded logic embedded in policy admin systems.

This programme is known internally as Prism.

### About Prism
Prism is a platform designed to standardise how pricing models are built, reviewed, versioned, and deployed. It is owned jointly by the actuarial, underwriting, and technology functions. The platform will serve multiple internal customers:
The Direct-to-Consumer business unit (e.g. for term life products sold online)
The Group Protection channel, which integrates via broker platforms
The Underwriting rules engine, which consumes pricing outputs downstream

The tech stack includes:

- .NET Core APIs for exposing model endpoints
- Python notebooks and pipelines for model development
- Azure DevOps for CI/CD
- AKS (Kubernetes) for deployment
- Terraform for infra provisioning
- Azure AppInsights and Splunk for observability


The architecture is sound, but governance remains fragmented:

- Business users submit Jira tickets to request pricing changes.
- Product Owners prioritise changes and escalate anything “risky” to risk and compliance.
- CAB approval is still required for all production changes, regardless of scope.
- Developers often work in shared repos but have limited access to production.
- Test environments are shared across teams and often out of sync.

### Governance Context

As a regulated insurer, Northbridge is subject to:

- FCA Principles for Businesses (especially Principle 3: due skill, care, and diligence)
- SMCR (Senior Managers & Certification Regime) - requiring clear accountability for decisions with material business impact
- Solvency II and internal model governance for pricing algorithms
- Internal audit and model risk teams, who require an evidence trail for every change that affects pricing outcomes

Historically, pricing changes were owned by actuarial teams, versioned manually, and deployed once per quarter - with paper-based sign-offs and narrative rationales in Word documents.

Prism is meant to change that - but it’s not yet clear how.

### Current Challenges

The Prism engineering team is capable and committed, but caught between conflicting expectations:

- CAB requires a full change pack for every deployment - even config-only changes.
- Actuarial SMEs expect to be “in the loop” but don’t understand Git, branches, or environments.
- Internal audit wants a PDF showing “who approved this change and why” - but engineers are reviewing and merging via PRs.
- Developers are expected to follow “team-owned” DevOps practices - but production access is restricted to a central ops team with a 2-day SLA for deployments.
- Security and architecture reviews are often requested reactively, delaying releases even when low risk.
- There is no clear way to track or flag the risk level of a change in a machine-readable format.

Despite best intentions, delivery is slow, uncertain, and highly manual.

### Stakeholder Perspectives

**Ritu Mehta (Platform Product Manager)** wants faster change delivery across multiple teams, but needs to balance this with satisfying compliance demands and cross-functional governance.


**Tim Blackwell (Senior Pricing Analyst)** wants visibility into what’s changing in the models and believes technical teams aren’t transparent enough. He’s frustrated by last-minute change approvals and audit requests.


**Olivia Harris (Engineering Lead, Prism)** wants to automate evidence collection and delegate approvals to domain experts, but feels blocked by compliance and risk functions who demand central sign-off.

**Phil Hammond (Head of Internal Audit)** expects to see a repeatable, documented process with clear approvals and traceability for any change that affects pricing, regardless of how minor.


### Your Assignment
Your group must design a new operating model for delivering changes in DeltaAssure - specifically for the SmartRate Engine team.

You should propose a system that:

- Manages change approvals and accountability
    - Who can approve what?
    - How are decisions logged?
    - What qualifies someone to approve a change?
- Delivers changes safely
    - How do changes go from dev to prod?
    - How do you handle different types of changes: code, config, model, data?
- Produces audit-ready evidence
    - What gets recorded?
    - How do you prove controls were followed?
    - What would you show an FCA auditor or internal audit team?
- Stays effective over time
    - Who reviews controls?
    - How do you know if a control is doing anything?
    - How would you know if it’s being bypassed?

You don’t need to write policy or code. But your solution should be drawn or mapped out visually and explain:

- The flow of a typical change
- Who approves what, and where
- What gets logged or enforced automatically
- Where humans still play a role
