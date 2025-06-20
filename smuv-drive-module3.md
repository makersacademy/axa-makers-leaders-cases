### SmuvDrive

SmuvDrive (prononced 'smooth drive') is a platform which connects people owning
cars or other utility vehicles (owners) with people who are looking to rent
vehicles for a short time (renters). One of the main selling points is that it
provides both the rental and the insurance cover for an all-inclusive solution.

The platform provides its own self-serve platform for individual users, but also
an API which other companies, called 'enterprise' customers (car rental
agencies, travel agencies, booking websites, etc.) can integrate with, so they
can provide a similar 'white label' experience within their own website.

*The business model*: SmuvDrive takes a small fee out of the total amount paid
by renters for the service, on top of the insurance cover price.

It also takes a larger fee from enterprise customers integrating with its API,
offering more flexibility and options as part of the insurance, depending on the
contract and options agreed with account managers.

Because of the premium cost, SmuvDrive offers SLA (Service Level Agreements) to
its enterprise customers to guarantee a minimum level or service, or offer
compensation in case these are not met.

These past years have been incredible good for SmuvDrive – the investment in
product, marketing and sales allowed it to grow at an incredible pace. However,
this rapid growth came at the cost of technical debt, causing a range of bugs
and failures in a system which is becoming increasingly complex.

This resulted
in loss of trust from both individual users but also enterprise customers, and
financial loss due to unmet SLAs compensation. Senior leaders are increasingly
concerned that the FCA (Financial Conduct Authority) will start looking into
this if problems keep happening. To make things worse, two of the most important
enterprise customers who had a long-term relationship with SmuvDrive are
starting to express concerns about the reliability of the platform. 

One the main areas where this technical debt shows today is in the lack of
observability on the platform. This problem is becoming so critical that a
dedicated 'task force' team has been created to address the problem.

This team? You guessed it, it's you.

Your goal will be to plan and collaborate with other teams, with the goal of
implementing a strong monitoring and incident response strategy across the wider
engineering team.

## Components deep drive

This is the current setup for the company infrastructure – most of it is running
on the cloud:

- **Gateway and Load Balancer** - the main 'entrypoint' for any client request
  coming from the Internet. Any HTTP request first gets through the Gateway and
  gets routed to one of the other components. The team owning this component is in the process of deploying big infrastructure changes on a tight deadline, and you've been informally told that any other not-urgent work likely 'won't happen in the next 3 to 6 months'.

- **Primary Database and Stand-by Database** – the main datastore and the
  'source of truth' for the data, a PostgreSQL database. It contains all user
  and vehicle data. No client request directly goes to the database, only other
  Services can 'talk' to the database. 
- **ElasticSearch cluster** – a full-text search software deployed on a cluster
  of machines. This is optimised to answer complex queries such as 'find all
  5-seat cars in Bristol, UK, for a trip between the 4th and the 8th of June,
  for a price no more than £40/day' – which search services such as
  Elasticsearch (ES) can deal with with higher performance than a relational DB.
  Here again, no client talks directly to ES, only other Services can query it.
- **Main API Service** - can respond to common API queries such as getting
  information for a specific vehicle, a user, etc.
- **Search Service** - used to search through the catalog of vehicles available
  to rent. This connects to both the ElasticSearch cluster as well as the main
  database to respond to clients.
- **Payment Service** - used to manage and process payments. It doesn't directly
  deal with customer credit cards and banks, but connects to a third-party
  payment service processor. This service contains a lot of legacy code, and due to the critical aspect of it, the team owning it isn't keen on letting other engineers work on it. It's usually quite a tedious process to suggest and deploy changes to this component for external teams.

- **Background job Workers** – these processes run on the same machines as the
  Main API Service. It's used to run asynchronous jobs which don't need to be
  executed immediately, but can afford a small delay – such as sending an email,
  generating an invoice, etc.
- **Web application Servers** – used to serve the SmuvDrive website to users
  accessing it by entering smuvdrive.co.uk in their web browser. The website is
  a React frontend which sends requests to other components and API services
  through HTTP.
- **Cache server** - used to cache results of common queries to improve
  performance.

API services machines are deployed and split across two geographic availability
zones (AZs) on the cloud provider for redundancy and high-availability.

This architecture is summarised in the diagram below:

![Architecture
diagram](https://eu-west-2.graphassets.com/AXI7KNWwuTwCtIHy5bFnWz/cmc4lcq3eg3eh07mhqdhfg82k)

## 1. Design monitoring 

**For each component, define key metrics and signals to monitor.**

You won't be able to do everything here. Remember the four 'golden signals' of
monitoring and the three 'pillars' - how can this inform your choice or what to
observe? Are some metrics more important than other? Why?

- Add challenges (technical but also operational, from team priorities conflict,
  etc) – find some conflicts here

## 2. Implement monitoring

- Define a strategy for your team to implement monitoring in the different components. Which services should you prioritise? Why?

- How will you deal with conflicts of priorities in the other teams owning each of the different components?

## 3. Define incident response strategies

- Imagine possible scenarios where something goes wrong in the system – at least
  one per component. How should the team react to such events, and how should
  they prioritise the work to make things go back to normal?

- How can you make sure you implement [root cause
  analysis](https://www.elastic.co/what-is/root-cause-analysis) as part of your
  incident response strategy?

In incident response, some common metrics are:
1. **RTO** (Recovery Time Objective) – which is the time the organisation can afford
   to get the system back available
2. **RPO** (Recovery Point Objective) – which is the amount of data which we can
   afford to lose in case of a failure
3. **MTTR** (Mean Time to Repair) - the approximate time between time of a failure
   and the time where it gets resolved

Different components or services can have different values for these metrics,
depending on how critical they are. How would you define yours?

## 4. Assess your strategy (presentations)

You will now have to present your solutions. The rest of the team will ask questions and probe for some things to make sure your strategy and design is battle-tested, or point out where it might need improvements.

