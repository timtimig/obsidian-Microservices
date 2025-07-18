## Microservices at a Glance

Microservices are independently releasable services that are modeled around a business domain. A service encapsulates functionality and makes it accessible to other services via networks.
Internal implementation details (such as the technology the service is written in or the way data is stored) are entirely hidden from the outside world.

Microservice architectures **avoid the use of shared databases** in most circumstances; instead, each microservice encapsulates its own database where required.

Microservices embrace the concept of information hiding. _Information hiding_ means **hiding as much information as possible** inside a component and exposing as little as possible via external interfaces. Implementation that is hidden from external parties can be changed freely as long as the networked interfaces the microservice exposes don’t change in a backward-incompatible fashion.

#### SOA
_Service-oriented architecture_ is a design approach in which multiple services collaborate to provide a certain end set of capabilities. A _service_ here typically means a completely separate operating system process. Communication between these services occurs via calls across a network rather than method calls within a process boundary.
I’ve seen plenty of examples of SOA in which teams were striving to make the services smaller, but they still had everything coupled to a database and had to deploy everything together. Service oriented? Yes. But it’s not microservices.
The microservice approach has emerged from real-world use, taking our better understanding of systems and architecture to do SOA well. You should think of microservices as being a specific approach for SOA in the same way that Extreme Programming (XP) or Scrum is a specific approach for Agile software development.

## Key concepts
###### 1. Independent Deployability
**It's the most important concept.**
_Independent deployability_ is the idea that we can make a change to a microservice, deploy it, and release that change to our users, without having to deploy any other microservices.
We need to make sure our microservices are _loosely coupled_.
Some implementation choices make this difficult—the sharing of databases, for example, is especially problematic.
The desire for loosely coupled services with stable interfaces guides our thinking about how we find our microservice boundaries in the first place.
###### 2. Modeled around a Business Domain
By modeling services around business domains, we can make it easier to roll out new functionality and to recombine microservices in different ways to deliver new functionality to our users.
Rolling out a feature that requires changes to more than one microservice is expensive. That takes a lot of more work than making the same change inside a single service. By making our services end-to-end slices of business functionality, we ensure that our architecture is arranged to make changes to business functionality as efficient as possible.
###### 3. Owning their own state
**Avoid to use of shared database**.
By hiding the database that backs our service, we also ensure that we reduce coupling.
###### 4. Size
The least interesting aspect and depends to context.
#### Alignment of architecture and organization
One approach is having layered horizontal architecture. When frontend developers and UI service in one team, a backend service in another, database in the third.
Instead this we can use vertical business lines. We see a dedicated team that has full-end-to-end responsibility for making changes: a **stream-aligned team**.

## The Monolith
When we are talking about monoliths here, we refer to a unit of deployment. There are several types like single-process monolith, modular, distributed. But if it must be deployed together is remains monolith.
A distributed monolith has all the disadvantages of a distributed system, and the disadvantages of a single-process monolith, without having enough of the upsides of either.

## Enabling Technology
No need to adopt lots of new technology when first start using microservices. You should constantly be looking for issues caused by your increasingly distributed system, and then for technology that might help.
#### Log aggregation and Distributed tracing
These systems allow you to collect and aggregate logs from across all your services, providing you a central place from which logs can be analyzed, and even made part of an active alerting mechanism.
You can make these log aggregation tools even more useful by implementing correlation IDs, in which a single ID is used for a related set of service calls.
As your system grows in complexity, it becomes essential to consider tools that allow you to better explore what your system is doing, providing the ability to analyze traces across multiple services, detect bottlenecks, and ask questions of your system that you didn’t know you would want to ask in the first place.
#### Containers and Kubernetes
_Containers_ provide a lightweight way to provision isolated execution for service instances. After you begin playing around with containers, you’ll also realize that you need something to allow you to manage these containers across lots of underlying machines. Container orchestration platforms like Kubernetes do exactly that.
But do your best to ensure that someone else is running the Kubernetes cluster for you, perhaps by making use of a managed service on a public cloud provider. Running your own Kubernetes cluster can be a significant amount of work!
#### Streaming
Although with microservices we are moving away from monolithic databases, we still need to find ways to share data between microservices.
**Apache Kafka** has become the facto choice for streaming data in a microservice environment.
**Debezium** is an open source tool developed to help stream data from existing datasources over Kafka, helping ensure that traditional datasources can become part of a stream-based architecture.
#### Public cloud and serverless
Public cloud providers offer a host of managed services, from managed database instances or Kubernetes clusters to message brokers or distributed filesystems.
Of particular interest among the public cloud offerings are the products that sit under the banner of _serverless_. These products hide the underlying machines, allowing you to work at a higher level of abstraction.
## Advantages of microservices
#### Technology heterogeneity
With a system composed of multiple microservices we can decide to use different technologies inside each one.
Also the fact that internal technology implementation is hidden from consumers can also make upgrading technologies easier.
#### Robustness
 A component of a system may fail, but as long as that failure doesn’t cascade, you can isolate the problem, and the rest of the system can carry on working.
 We do need to be careful, however. To ensure that our microservice systems can properly embrace this improved robustness, we need to understand the new sources of failure that distributed systems have to deal with. Networks can and will fail, as will machines.
#### Scaling
With a large, monolithic service, we need to scale everything together. Perhaps one small part of our overall system is constrained in performance, but if that behavior is locked up in a giant monolithic application, we need to handle scaling everything as a piece. With smaller services, we can scale just those services that need scaling, allowing us to run other parts of the system on smaller, less powerful hardware.
#### Easy of deployment
A one-line change to a million-line monolithic application requires the entire application to be deployed in order to release the change. This means that our changes continue to build up between releases, until the new version of our application entering production has masses of changes. And the bigger the delta between releases, the higher the risk that we’ll get something wrong!
With microservices, we can make a change to a single service and deploy it independently of the rest of the system. This allows us to get our code deployed more quickly. If a problem does occur, it can be quickly isolated to an individual service, making fast rollback easy to achieve.
#### Organizational alignment
Smaller teams working on smaller codebases tend to be more productive. Microservices allow us to better align our architecture to our organization, helping us minimize the number of people working on any one codebase to hit the sweet spot of team size and productivity.
#### Composability
One of the key promises of distributed systems and service-oriented architectures is that we open up opportunities for reuse of functionality. With microservices, we allow for our functionality to be consumed in different ways for different purposes.
We need to think of the myriad ways that we might want to weave together capabilities for the web, native application, mobile web, tablet app, or wearable device. With microservices, as circumstances change, we can build applications in different ways.