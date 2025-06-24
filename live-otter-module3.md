### LiveOtter

LiveOtter is a platform which sells concert and events tickets. The platform is actually two different products:
- The 'public' user-facing product, which is a mobile and web application available to the general public – people can use to search and browse for events (by keywords, date or venue, for example).
- The self-serve software as a service (SaaS) platform, which promoters can use to create and manage events before they're available on sale to the general public on the user-facing application.

Both these applications rely on the same backend system which centralises logic and data. The backend is almost entirely hosted on a cloud platform (aside a few legacy components not yet migrated, still running on the company's on-premises servers). It uses a relational SQL database as its main data store, as well as an 'in memory' smaller database which is used to cache recently used data and improve performance. Additionally, a full-text search service is used to allow search by keywords and data in the large number of available events.

Below is a diagram illustrating the overall system architecture:

![Diagram of the LiveOtter cloud architecture](https://eu-west-2.graphassets.com/AXI7KNWwuTwCtIHy5bFnWz/cmbq8w6jd11nw07l684nuq919)

**The team**

- **Jay (Product Manager)**: Jay has recently joined the team as product manager and is under pressure to balance key stakeholders needs and team resourcing. 
- **Kiera (Backend Engineer, Senior)**: Kiera has been in a team for a while and, due to her experience, she is often busy reviewing code or discussing the design and implementation or larger features. She spends about 30% contributing and 70% in other management or high-level design work.
- **Maxwell (Backend Engineer, Junior)**: Maxwell has joined recently and is a great addition to the team.
- **Nora (Platform Engineer, Mid-level)**: Nora has been working for a few years, her time is spent between fire-fighting any incidents which might happen in production, while migrating the remaining components of the system onto the cloud provider.

**Wednesday 4th of June – Message thread:**

(...)

**Jay:** Remember that this *Friday morning at 10am* is when tickets for **you know who** will be released on sale. This is a major deal for us, probably the biggest yet – about 100k users registered to be notified when the sale starts. Are we confident the system will be able to handle the load?

**Kiera:** Hey, Jay – that sounds exciting. We made a lot of work recently to make our backend code more efficient, and we improved the way we interact with the database to make sure it'll be able to handle even this many people connecting at once. Maxwell actually just shipped his second ticket, which is also improving the performance by leveraging our cache, and should make the event screen load faster! I also think Nora was doing some work on the infra side just to make sure we're covered there.

**Jay:** Sounds all fantastic. Hey @Nora can you confirm whether you think the infrastructure will be OK as well with that load?

**Nora:** Hey, indeed I've just merged a PR which gives us more flexibility in configuring how many API servers we need. This way we can set it up to scale out at a given time – I'm gonna do this for Friday, and double or usual number of servers. According to my rough calculations, this should be more than enough to handle even 50% more of that many users.

**Jay**: Great, sounds like we're all set!

(...)

**Thursday 5th of June – Message thread:**

**Jay**: Hey team, just checking in – our account managers got emails from two different promoters telling that the SaaS platform has been a bit slow in the last few days. Did we release anything new?

**Kiera**: Hey Jay, no we didn't – we're actually now holding off any releases until after the go live tomorrow to avoid any last-minute problems. Did they say anything more on the problems they experienced?

**Jay**: Hmm no. Just that it was slow.

**Kiera**: OK. Maybe it's just a transient thing, let's see. Let us know in case it happens again!

**Friday 6th of June (Go-live day - minutes before 10am) – Message thread:**

**Jay**: Hey team, I know it's probably not the right time but... Still got more people complaining about the SaaS UI. Apparently it's so slow that some of them can't even do basic work such as editing an even. Can anyone look into this? @Nora do we have enough servers to handle the load?

**Nora**: Hey Jay, yeah definitely – we've now doubled our capacity so there's no way it can be because of this. Again did they mention anything more specific? I don't think we released anything, right @Kiera?

**Kiera**: No indeed. Not sure what it can be – I'm happy to look into this, but again we won't be able to deploy any bug fix until after the go-live this morning.

**Jay**: OK. Well, it's only a few minutes away. Let's cross fingers... 

(...)

**Jay**: OK this doesn't look good. A few people in the team have tried getting tickets and mention the app is completely unresponsive. Also some people are starting to complain on social media they can't get tickets. Do we know what's happening?

**Kiera**: Yes we're seeing it as well. Maybe we underestimated the server capacity. @Nora is there a way we can launch more machines?

**Nora**: I'm on it. I'm updating our auto scaling servers pool so it should be just a few minutes before things get better.

**Jay**: Ok fantastic. Thanks! We'll try again on our side and I'll coordinate with the team to manage expectations on social media etc. 

**10 minutes later – face-to-face conversation in the office:**

**Jay:** This doesn't seem to get better :(

**Nora**: OK, it's gonna be a slower but I'm gonna attempt to login by SSH into different machines and inspect system metrics to see what might be the problem. It could be that we're overloading the CPU somehow, or that we have some buggy code causing memory leaks, even if *in theory* we should have enough servers...

**Kiera**: But again, we didn't release anything – so surely we should've seen these problems before, no? I mean... we didn't release anything, *right*, Maxwell?

**Maxwell** (shrugs): Don't think so. But I'm gonna have a look through the list of recent commits, just to...

**Nora**: Oh. I think I found it.

**Kiera**: What?

**Nora**: It's one of our search service nodes.

**Kiera**: Well, what's up with it?

**Nora**: Its disk is full.

(Silence.)

**Kiera**: So it will prevent some data to be indexed. And might cause a snowball reaction which leads the whole search service to be unresponsive... But I don't get it, even if users can't search for events on the app, they should still be able to get a ticket and place the order, right?

**Jay**: Yeah, this doesn't make sense.

**Maxwell**: No, it does actually. When the app launches, we're loading the list of events from the API in the background. I think this might call the search service under the hood. So it means that, even if the user is on a different screen, this API endpoint will be called. So if the search service is down...

**Nora**: Then the whole app is down.

(Another silence.)

**Nora**: I'm going to upgrade the disk for the new code and pick a bigger volume, then I'll upgrade our search cluster. This should be done in about 15 minutes, but... I don't think it can be faster than this.

### Questions

We might not have the time to cover all of the questions below, and that's OK. Each of them is open-ended and can prompt a discussion to gain better insights into the LiveOtter's current processes and potential improvements. Feel free to use these prompts as a tool to reflect on the case presented above, but also to apply them to some scenarios you might pick from your own experience.

- How observability could have prevented such a scenario to happen? What signals the team could have used to understand that failure was about to happen?

- All these engineers are competent – although they wrongly assumed, in this case, that scaling the API layer with more machines would resolve the problem. Put yourself in their shoes: why do you think they made this assumption? Can you find any similar cases from your own experience where wrong assumptions were made and prevented a problem to be resolved quickly?

- A 'single point of failure' (SPOF) or a 'bottleneck' in a system is a component which can cause the entire system to fail if it fails itself. Their presence is usually a key reason why complex software systems fail. How, in this case, a single point of failure caused a problem? Can you see any other potential SPOF in this system which engineers should have a look at?

- There are a few mentions of work being done to make the backend 'more efficient' or the database 'handle even this many people connecting at once', etc. Without observability, what can be the issues here? If this were your team, what could you suggest, as a technical leader, to improve the way they're working on improving performance of systems they work on?

- How might the interconnected nature of LiveOtter's backend systems (SQL database, in-memory cache, search service) complicate the monitoring and identification of performance bottlenecks? What strategies could be employed to better isolate and diagnose issues in such a complex architecture?

- Throughout the case, the team appears to react to issues as they arise. What proactive monitoring strategies could have been implemented to anticipate and mitigate the problems encountered during releases?

- Evaluate the team's communication and incident response process during the outage. What improvements could be made to ensure more effective coordination and faster resolution of issues in the future?

- After resolving the outage, what steps should the team take in a post-incident review to learn from the experience and implement changes that will prevent similar issues in the future? What metrics and data should be collected during incidents to facilitate this review process?
