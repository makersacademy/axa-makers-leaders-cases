## **Tyne and Wear Digital Transport Infrastructure Project**

You work for Newcastle’s Department of Smart Transport, which is responsible for developing and maintaining the digital services supporting the Tyne and Wear Metro Network. The department is modernising its systems to improve real-time travel information, passenger experience, and overall network efficiency.

The workstream you’re part of is structured into ****three specialist teams, each responsible for a key part of the system:

- **Passenger Information Service** – Provides real-time updates on train schedules, platform changes, and service disruptions. This service powers mobile apps and station displays.
- **Monitoring & Analytics Service** – Tracks train locations, system performance, and crowding levels. This data is used for operational decision-making, predictive maintenance, and improving passenger flow.
- **Transport Infrastructure Platform** – Provides core services such as APIs, authentication, data pipelines, and messaging infrastructure to support the other teams.

Each team has clear ownership, but all three must work together to deliver a reliable and efficient transport experience. Your team will take responsibility for one of these services, collaborating with the others to ensure seamless integration. Here’s an overview of each service:

### **1. Team Shearer: Passenger Information Service**

This team is **Stream-Aligned.** These are teams aligned to a continuous flow of work from a specific business domain or customer need.

**Responsibilities**

- Provide real-time updates on train schedules, delays, and platform changes to passengers via mobile apps and station displays.
- Offer route planning and alternative suggestions based on system conditions.

**Dependencies**

- Relies on the Monitoring & Analytics Service for train tracking and crowding data.
- Uses the Platform Team’s APIs and infrastructure.
    
    
**Your priorities**

**Usability, performance, and quality.** The service must be intuitive and accessible to a diverse range of passengers, ensuring information is easy to find and understand. Speed is critical—real-time updates must be delivered with minimal latency to keep passengers informed of changes as they happen. Performance involves maintaining system reliability even during peak travel times, ensuring that apps and displays remain responsive. Quality encompasses the accuracy of information provided, reducing errors and ensuring consistent, dependable communication with passengers.

### **2. Team Keegan: Monitoring & Analytics Service**

This is a **Complicated Subsystem** team. These teams are responsible for areas of the system requiring deep expertise and specialised knowledge.

**Responsibilities**

- Track train positions, system health, and passenger congestion using IoT devices (GPS & environmental monitors on trains, LIDAR in stations, data transferred over either cellular or WiFi where available).
- Manage IoT functionality through Azure IoT Hub.
    
    

**Dependencies**

- Must make data available as close to real-time as possible for Passenger Information Service.
- Relies on the Platform Team for infrastructure services and API layer.

**Your priorities**

**Data quality and reliable integrations with hardware**. Ensuring high data quality is essential for accurate tracking, predictive maintenance, and reliable passenger information. Integrations with hardware such as IoT sensors must be seamless and robust to provide continuous, real-time data streams. Reliability is critical, with systems needing to function consistently even during peak hours or unexpected network disruptions. Speed in both data processing and delivery ensures that operational decisions and passenger updates are based on the most current information available.

### **3. Team Ginola: Transport Infrastructure Platform**

This is a **Platform** team. These teams create and manage internal services, tools, or platforms to be used by other teams.

**Responsibilities**

- Provide core infrastructure services for other teams.
- Design and manage APIs used by the other teams.
- Offer scalable, resilient, and secure compute/storage for applications.

**Dependencies**

- Manages access control for the other services, ensuring secure data handling.
- Acts as the backbone for event-driven messaging, ensuring all teams can publish/subscribe to critical transport events.

**Your priorities**

**Stability, uptime, security, and keeping costs down**. Ensuring platform stability is crucial so that core services like ticketing and data pipelines function reliably without unexpected interruptions. Uptime is a priority, with the expectation of near-continuous service availability to support both passengers and operational systems. Security must be robust to protect sensitive passenger data and prevent unauthorised access to critical transport infrastructure. Keeping costs down involves optimising resource usage and infrastructure scalability, ensuring high performance without unnecessary expenditure.

## Your Assignment

Each team will need to produce two things:

1. A design of some kind for your part of the system. You can choose the format: it might be an architecture diagram, a flow diagram or a description of your proposed approach. It **must** make sense alongside the work of the other two teams. No siloes! You’ll almost certainly need to speak to the other teams to complete this.
2. A plan for how you will work with the other two teams including when you’ll meet and how you’ll manage tasks together. Consider the three modes of interaction we discussed this morning:
    1. **Collaboration**: Teams work closely together for a period to solve a complex problem, develop a shared understanding, or create something new. Good for high uncertainty tasks, early in a project, or when shared context is critical.
    2. **X-as-a-Service**: One team provides a service (e.g., a platform, tool, or API) to another team, typically through a clear interface or contract. Good for routine, repeatable interactions that benefit from standardisation and scalability.
    3. **Facilitating**: One team helps another by transferring knowledge, removing obstacles, or enhancing their skills and capabilities. Useful when a team needs guidance or support to work autonomously in the future.

You can use whatever tools you like to create your plans. You might consider
using [draw.io](https://www.draw.io), [Excalidraw](https://www.excalidraw.com/),
[Miro](https://www.miro.com), [Archi](https://www.archimatetool.com), or
something else.

## Stakeholders

**Peter O'Hanrahan, North East Mayor**

Peter is a proud Geordie and strong ambassador for the city. He wants to boast about the hi-tech metro system and show it off to his peers. He’ll value things working as they should.

**Samir Evans, Department CTO**

Samir is a laser-sharp CTO but tends to panic if things seem out of control. He will be particularly focussed on documentation and the sensible use of resources (especially money).

**Geoff Linton, Rail Passenger**

Geoff is a regular commuter on the network who relies on the metro to get to work. He hates a busy or dirty train and so he’s excited to use the app to understand which service to get.

