**Project Overview**

The Payments Manager is a legacy on-prem monolith that handles late payments and payment plans. It integrates with three external SOAP services and one external RESTful JSON API. The application’s codebase is a mix of messy, undocumented “big ball of mud” sections and clean, well-documented modules. It’s generally well-tested but suffers from intermittent performance issues: occasional lost or timed-out requests and a lack of consistent monitoring. Payments Manager is consumed by another, user-facing system. A new version of this is due to go live in 6 months, and stakeholders are pressuring Tech Lead Maya to consider migrating the project to Azure before this happens to address current challenges.

**The Team**

- **Maya (Tech Lead):** Competent and motivated, alternates between optimism and worry about the project. Maya is under pressure to deliver and struggles to balance stakeholder expectations with team capacity.
- **Zane (Full Stack, Mid-level):** Enthusiastic about tools and new technologies but can underestimate complexities. Likes to get on with things.
- **Priya (Front End, Mid-level):** Pragmatic leaning to cautious, worries about workload and her preparedness.
- **Carlos (Back End, Senior):** Deeply knowledgeable about the on-prem system, can seem resistant to change. Confident in improving the current setup.

**Tuesday 12 June, 3.30pm, a Teams call:**

[…]

**Maya:** OK, let’s chat migration now. I'll give you a bit of an update on where we are and then it would be good to hear from everyone. Delivery have confirmed the new platform is going live in November. We’re under some pressure now to figure out the best path forward for Payments Manager. Let’s use this time to discuss our options. The big question is whether to migrate it to Azure now, improve it on-prem, or…something else. Let’s hear your thoughts.

**Zane:** I’ll start. You guys know what I think. Azure is a no-brainer. We can leverage stuff like Azure Functions for event-driven workflows, Logic Apps to streamline the integrations, and Cosmos for the database. These tools will fix our scaling issues and reduce latency. Plus, Azure Monitor and Application Insights would hugely improve our observability, which is something we’re lacking right now. Six months isn't even tight, it’s totally doable.

**Carlos:** Zane, that sounds nice, but have you really thought this through? In my experience re-architecting a monolith isn’t just flipping a switch—it’s a minefield. We’d risk breaking the integrations, losing data, and blowing the timeline. We’d be dealing with migration risks, compatibility issues, and the learning curve. I’m not convinced it’s worth the gamble, especially when the on-prem setup can be tuned up.

**Zane:** Tuned up? It’s a patchwork of spaghetti code in places! Migrating would force us to clean it up. Plus, we’d be future-proofing. On-prem is a dead end.

**Priya:** I’m with Carlos on the risks. Migration sounds exciting, but we can’t underestimate the effort. I’ve seen a migration project like this at my last job fall apart because we underestimated how much work it would take to refactor legacy integrations. We spent months chasing compatibility issues and still ended up with performance hiccups. Six months isn’t just tight—it feels impossible without cutting corners. The front end alone might need major changes. Do we even know how the integrations will hold up? And what about testing? Six months feels like a pipe dream.

We don’t have a clear roadmap. We need to map dependencies, test migration paths, and account for surprises. The timeline worries me.

**Maya:** Good points. Are we sure we even understand the full scope of the current issues? Without better data on what’s causing the timeouts and lost requests, how do we confidently propose any path forward? If we jump into the migration without clarity, we’re maybe just setting ourselves up to fail. I know monitoring is still patchy, what data do we have on timeouts and lost requests?

**Carlos:** Not enough, honestly. That’s why I think we should fix the monitoring first. Improve visibility, address bottlenecks, and optimize performance on-prem. The system isn’t perfect, but it’s functional. We’d be taking a huge risk by tearing it down without understanding the root problems.

**Zane:** But fixing monitoring doesn’t solve the bigger issue: scalability. The new product’s load will cripple the app. We need elasticity, and the cloud gives us that.

**Priya:** Assuming we have time to re-architect and test under load. I’m worried about the integrations. Those SOAP services…are we even sure they’ll work seamlessly in Azure?

**Maya:** A phased approach might work, but that doesn’t answer the cost question. Stakeholders want a decision soon because of renewal costs. Can we justify staying on-prem if we’re about to invest in upgrades?

**Carlos:** We’d spend less improving monitoring and tuning performance than migrating everything. Azure has costs too—not just migration, but ongoing expenses. Plus, I’m skeptical we can meet the timeline.

**Zane:** Costs aside, we’re setting ourselves up for future agility. Staying on-prem is short-sighted. We’d be solving today’s problems but creating tomorrow’s.

**Priya:** Tomorrow’s problems sound a lot like today’s if the migration fails. We need to ask ourselves what's actually feasible in six months.

**Maya:** That’s the big question. I have to run to another meeting — I'll follow up on Teams later.

---

**Questions**

Where do your sympathies lie? Do you find yourself leaning one way or another?

Put yourself in Maya's shoes: what would your next steps be?

Where are the risks in the team's thinking?

Where are the risks in the project as a whole?