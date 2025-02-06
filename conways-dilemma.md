*"It’s not our job to fix their mess, Jamie,"* Ravi says, leaning back in his chair. His screen is filled with error logs from the latest deployment. The API Gateway is timing out, and no one can agree on whose responsibility it is to fix it.

This is the third incident this month related to the new transaction processing system—a project that was supposed to be straightforward but has turned into a slow-moving headache.

## **The Project**

FinLight Solutions Ltd, a fast-growing financial technology company, specialises in providing seamless payment processing services for SMEs. The company is modernising its payment platform, migrating from an ageing on-prem system to a cloud-based architecture. The project was greenlit six months ago, with the expectation that it would improve processing speed and reduce downtime. The new architecture consists of microservices for transaction intake, processing, and validation, all communicating through an API Gateway. A combination of serverless functions and containerised services handle various processing tasks, while a central event-driven system orchestrates workflows between internal systems and third-party providers.

Engineering built the microservices, Platform Engineering owns the cloud infrastructure, and Quality Engineering (outsourced) is responsible for end-to-end testing. But with each team working in silos, issues keep slipping through the cracks.

Jamie, a tech lead in Engineering, has been caught in the middle. She owns the transaction intake service, which is one of the core components in the architecture, but has no direct authority over Platform or QA. She spends more time in meetings than writing code, trying to align expectations across teams.

Yesterday, an issue made it to production: transactions submitted via the new system weren’t syncing properly with downstream legacy systems. Specifically, an event message carrying transaction data failed to reach the legacy account management system, causing payments to remain in a 'pending' state indefinitely. The root cause isn’t clear—Engineering suspects a schema mismatch, while Platform Engineering believes the issue is related to an intermittent connectivity problem in the API Gateway.

The CEO, frustrated, wants an explanation and a plan to stop this from happening again. The post-mortem is in an hour, and Jamie knows it’s going to be a mess.

---

## **Jamie (Engineering Tech Lead)**

*"I’m tired of playing middleman. Every time something goes wrong, it’s ‘Engineering needs to fix this.’ But half these problems come from integration issues we don’t even control. The Platform team built a new API Gateway, but they never gave us proper documentation. And QA? They barely test edge cases before signing off on releases. I get why—they’re outsourced, so they aren’t incentivised to dig deep. But I’m the one who has to explain why things keep breaking."*

*"At the same time, I don’t know what the alternative is. I don’t have authority over these teams, and leadership isn’t going to step in to fix this. We all just do our part and hope it fits together in the end. And clearly, it doesn’t."*

---

## **Ravi (Senior Platform Engineer)**

*"Engineering keeps throwing problems over the fence like it’s our fault. Yeah, the API Gateway had some latency issues, but they never tell us when their changes could impact our configurations. The real issue? There’s no clear ownership model here. Who’s accountable for integration? Who makes the final call on release readiness? Right now, everyone assumes someone else is checking. I get why Jamie’s frustrated, but I’m just as tired of firefighting problems that could’ve been caught with better coordination."*

*"I don’t think anyone is trying to make this harder than it needs to be. But the way things are set up, what are we supposed to do? We all have our own teams, our own priorities, our own deadlines. No one has time to sit in endless meetings to sync up every little thing. We just hope for the best and deal with the fallout when things go wrong."*

---

## **Lisa (QA Lead, Outsourced Team)**

*"I see the problems. I really do. But our contract is built around test cases, not continuous engagement. We aren’t in the planning meetings. We don’t have visibility into real-time changes. We test what’s in front of us, and if the requirements are unclear, we assume they’re correct."*

*"Could we be more proactive? Maybe. But no one’s asking us to be. And honestly, when we do flag things, it’s usually too late—decisions have already been made. I can already predict how this post-mortem is going to go. Engineering will say QA missed something. Platform will say the problem wasn’t theirs. And nothing will change."*

---

## **The Tension**

Jamie knows this post-mortem will go one of two ways: either it becomes a blame game, or it sparks a real conversation about team responsibilities.

She also knows that team structures shape behaviour. The current model—where Engineering, Platform, and QA operate in silos—virtually guarantees misalignment. Jamie had been reading about Conway’s Law recently, and it kept resurfacing in her mind. The way teams communicate and collaborate—or fail to—inevitably shapes the software they build. The fragmented nature of the payment platform wasn’t just an accident; it was a reflection of how Engineering, Platform, and QA operated in their own silos. If they didn’t change how they worked together, they would keep running into the same problems, no matter how many post-mortems they held.

But changing how teams work together isn’t up to her.

She takes a deep breath and heads to the conference room.

---

### **Discussion Questions**

1. **Where does responsibility lie in this case?** Who should own integration testing and deployment readiness?
2. **How do team boundaries and communication contribute to the ongoing issues?**
3. **If you were Jamie, how would you approach the post-mortem?**
4. **Given that no one in this scenario has the power to change the org structure, what *small* changes could they make to improve collaboration?**
5. **How can feedback loops be improved between teams, even with an outsourced QA function?**