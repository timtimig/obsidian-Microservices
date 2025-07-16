Microservices are independently releasable services that are modeled around a business domain. A service encapsulates functionality and makes it accessible to other services via networks.
Internal implementation details (such as the technology the service is written in or the way data is stored) are entirely hidden from the outside world.

Microservice architectures **avoid the use of shared databases** in most circumstances; instead, each microservice encapsulates its own database where required.

Microservices embrace the concept of information hiding. _Information hiding_ means **hiding as much information as possible** inside a component and exposing as little as possible via external interfaces. Implementation that is hidden from external parties can be changed freely as long as the networked interfaces the microservice exposes don’t change in a backward-incompatible fashion.

#### SOA
_Service-oriented architecture_ is a design approach in which multiple services collaborate to provide a certain end set of capabilities. A _service_ here typically means a completely separate operating system process. Communication between these services occurs via calls across a network rather than method calls within a process boundary.
I’ve seen plenty of examples of SOA in which teams were striving to make the services smaller, but they still had everything coupled to a database and had to deploy everything together. Service oriented? Yes. But it’s not microservices.
The microservice approach has emerged from real-world use, taking our better understanding of systems and architecture to do SOA well. You should think of microservices as being a specific approach for SOA in the same way that Extreme Programming (XP) or Scrum is a specific approach for Agile software development.

#### Key concepts
###### 1. Independent Deployability
**It's the most important concept.**
_Independent deployability_ is the idea that we can make a change to a microservice, deploy it, and release that change to our users, without having to deploy any other microservices.
We need to make sure our microservices are _loosely coupled_.
Some implementation choices make this difficult—the sharing of databases, for example, is especially problematic.
The desire for loosely coupled services with stable interfaces guides our thinking about how we find our microservice boundaries in the first place.
###### 2. Modeled around a Business Domain
By modeling services around business domains, we can make it easier to roll out new functionality and to recombine microservices in different ways to deliver new functionality to our users.