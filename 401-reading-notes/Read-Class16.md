# **Serverless**

![serverless](https://1reddrop.com/wp-content/uploads/2019/01/Serverless.jpg)

Reading from [Serverless Website](https://www.ibm.com/cloud/learn/serverless#toc-what-isser-mqOIozfo)
Reading from [Serverless](https://canvas.instructure.com/courses/4333667/discussion_topics/14075571)



Serverless is a cloud execution model that enables a simpler, more cost-effective way to build and operate cloud-native applications.

## **What is serverless?**
Serverless is a cloud computing execution model that 

Automatically provisions the computing resources required to run application code on demand, or in response to a specific event;
Automatically scales those resources up or down in response to increased or decreased demand;
Automatically scales resources to zero when the application stops running. 
Serverless offloads all management responsibility for backend cloud infrastructure and operations tasks - provisioning, scheduling, scaling, patching and more - to the cloud provider. This gives developers more time to develop and optimize their front-end application code and business logic. And with serverless, customers never pay for idle capacity. They pay only for the resources required to run their applications, and only when those applications are running.

The name notwithstanding, there are most definitely servers in serverless computing. The term 'serverless' describes the customer's experience with those servers: they are invisible to the customer, who doesn't see them, manage them, or interact with them in any way.

Amazon Web Services introduced serverless in 2014 with AWS Lambda; today every leading cloud service provider offers a serverless platform including Microsoft Azure (Azure Functions), Google Cloud (Google Cloud Functions) and IBM Cloud (IBM Cloud Code Engine). Together serverless, microservices and containers, form a triumvirate of technologies typically considered to be at the core of cloud-native application development.

### **Serverless vs. FaaS (function as a service)**
Serverless and function as a service (FaaS) are often conflated. But FaaS is actually a subset of serverless - it's the compute paradigm central to serverless, wherein application code or containers run only in response to events or requests. Serverless includes FaaS plus all the other associated resources and cloud services and resources supporting the code - e.g. storage, databases, networks, API gateways, authentication - for which configuration, management and billing of services are invisible to the user.

## **Serverless pros and cons**

### **Pros**
Serverless offers a number of individual technical and business benefits:

- As noted above, serverless enables development teams to focus on writing code, not managing infrastructure. It gives developers much more time to innovate and optimize their front-end application functionality and business logic.
- Also as noted above, serverless customers pay for execution only. The meter starts when the request is made, and ends when execution finishes. Compare to the infrastructure as a service (IaaS) compute model, where customers pay for the virtual machines (VMs) and other resources required to run applications, from the time they provision those resources until the time the customer explicitly decommissions those resources.
- Serverless is a polyglot environment, enabling developers to code in any language or framework - Java, Python, node.js - with which they're comfortable.
- Serverless simplifies deployment and, in a larger sense, simplifies DevOps cycles, because developers don't have to describe infrastructure needed integrate, test, deliver and deploy code builds into production.
- For certain workloads, such as ones that require parallel processing, serverless can be both faster and more cost-effective than other forms of compute.
- Serverless application development platforms provide near-total visibility into system and user times, and can aggregate that information systematically.


### **Cons**
With so much to like about serverless computing, organizations are using it for a wide variety of applications (see Figure 2 below). However, there are certain applications for which serverless is not favorable, or which present technical and business trade-offs to consider:

- Stable or predictable workloads: Because serverless scales up and down on demand in response to workload, it offers significant cost savings for spiky workloads. But it does not offer the same savings for workloads characterized by predictable, steady or long-running processes; in these cases a traditional server environment might be simpler and more cost-effective.
- Cold starts: Because serverless architectures forgo long-running processes in favor of scaling up and down to zero, they also sometimes need to start up from zero to serve a new request. For certain applications, this startup latency isn’t noticeable or detrimental to users. But for others - for example, financial trading application - the delay is unacceptable.
- Monitoring and debugging: These operational tasks are challenging in any distributed system, but a move serverless architecture (or microservices architecture, or a combination of the two) only exacerbates the complexity. For example, teams may find it difficult or impossible to monitor or debug serverless functions using existing tools or processes.
- Vendor lock-in: Serverless architectures are designed to take advantage of an ecosystem of managed cloud services and, in terms of architectural models, go the furthest to decouple a workload from something more portable, like a virtual machine (VM) or Docker container. For some companies, deeply integrating with the native managed services of a specific cloud platform is where much of the value of cloud can be found; for others, this cloud lead to material lock-in risks that need to be mitigated.


## **Understanding the serverless stack**
Defining serverless as a set of common attributes, instead of as an explicit technology, makes it easier to understand how the serverless approach can manifest in other core areas of the stack.

- **Functions as a Service (FaaS)**: Again, FaaS is widely understood as the central/foundational compute/processing engine in serverless and sits in the center of most serverless architectures. See "What is FaaS?" for a deeper dive into the technology.
- **Serverless databases and storage**: Databases (SQL and NoSQL) and storage (particularly object storage) are the foundation of the data layer. A “serverless” approach to these technologies involves transitioning away from provisioning “instances” with defined capacity, connection and query limits, and moving toward models that scale linearly with demand in both infrastructure and pricing.
- **Event streaming and messaging**: Serverless architectures are well-suited for event-driven and stream-processing workloads most notably open source Apache Kafka event streaming platform.
- **API gateways**: API gateways act as proxies to web actions and provide HTTP method routing, client ID and secrets, rate limits, CORS, viewing API usage, viewing response logs, and API sharing policies.

## **Use cases for serverless**
Given its unique combination of attributes and benefits, serverless architecture is well-suited for use cases around microservices, mobile backends, and data and event stream processing.

- Serverless and microservices
The most common use case of serverless today is supporting microservices architectures. The microservices model is focused on creating small services that do a single job and communicate with one another using APIs. While microservices can also be built and operated using either PaaS or containers, serverless has gained significant momentum given its attributes around small bits of code, inherent and automatic scaling, rapid provisioning, and a pricing model that never charges for idle capacity.

- API backends
Any action (or function) in a serverless platform can be turned into a HTTP endpoint ready to be consumed by web clients. When enabled for web, these actions are called web actions. Once you have web actions, you can assemble them into a full-featured API with an API gateway that brings additional security, OAuth support, rate limiting, and custom domain support.

- Data processing
Serverless is well-suited to working with structured text, audio, image, and video data, around tasks such as data enrichment, transformation, validation, cleansing; PDF processing; audio normalization; image processing (rotation, sharpening, noise reduction, thumbnail generation); optical character recognition (OCR); and video transcoding. For a detailed image process use case, read “How SiteSpirit got 10x faster, at 10% of the cost.”

- Massively parallel compute/“Map” operations
Any kind of embarrassingly parallel task is a good use case for a serverless runtime, with each parallelizable task resulting in one action invocation. Sample tasks include everything from data search and processing (specifically Cloud Object Storage), Map(-Reduce) operations and web scraping to business process automation, hyperparameter tuning, Monte Carlo simulations and genome processing.

- Stream processing workloads
Combining managed Apache Kafka with FaaS and database/storage offers a powerful foundation for real-time buildouts of data pipelines and streaming apps. These architectures are ideally suited for working with all sorts of data stream ingestions (for validation, cleansing, enrichment, transformation), including IoT sensor data, application log data, financial market data and business data streams (from other data sources).