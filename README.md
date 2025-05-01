# Preface

- **Domain-Driven Design (DDD)** - A set of software **modeling tools**/patterns.
  - Drawing **_Context Maps_**.
  - Modeling the business process using **_Event Storming_**.

## What This Book Covers

### Strategic Tools (Design Phase)

- Chapter 2 - Foundation of DDD:
  - **_Bounded Contexts_**
  - **_Ubiquitous Language_**
- Chapter 3 - **_Subdomains_**
  - To deal with the complexity of integrating with existing **legacy systems**.
- Chapter 4 - **_Context Mapping_** (Diagram)

### Tactical Tools (Implementation Phase)

- Chapter 5 - Tactical modeling with **_Aggregates_**
  - Tactical modeling tool to be used with **_Aggregates_** is **_Domain Events_**.

# Chapter 1. DDD for Me

- Enabling us to perform at **scale**.
- **Strategic** tools
  - Can help you make **software design choices** and **integration decisions**.
- **Tactical** tools
  - Can help you **design** useful software that **accurately models** the business's unique operations.

## Will DDD Hurt?

- DDD is a set of **advanced techniques** to be used on **complex software** projects.
- **Note:** To learn DDD in **detail**, check out the **_Implementing Domain-Driven Design_** book.

## Good, Bad, and Effective Design

- **Nonexistent** design - No effort was put into software design, such as focusing only on completing the task/sprint board.
  - Uses **Scrum** to primarily control timelines rather than allow for one of Scrum's most important principles: **knowledge acquisition** (through **experimentation** and **collaborative learning**).
- **Common situations** caused by bad design:
  - Software projects are in **peril**, and entire teams are hired **to keep systems up and running**, **patching code and data** daily.
- **Potential problems** (ones that DDD can readily help teams avoid):
  - Developers trying to solve problems using technology **rather than careful thought and design**.
  - Database is given **to much priority** rather than business processes and operations.
  - Developers don't give proper emphasis to **naming objects and operations** according to the **business purpose**.
  - **Over-emphasis on project estimates** - Developers use the "task-board shuffle" rather than thoughtful design.
  - Developers house business logic in **user interface** components and **persistence** components.
    - \*Perform persistence operations in the middle of business logic.
  - **Broken**, **slow**, and **locking** database queries.
  - **Wrong abstractions**, where developers attempt to address all current and **imagined future needs** (Violating YAGNI) by **overly generalizing** solutions.
  - **Strongly coupled services** - Often leads to **broken business processes** and **unreconciled data**.
- Design is **inevitable**. The alternative to good design is bad design.

## Strategic Design (High Level, Big Picture)

- A context map of a bounded context:
  ![1-1-strategic-design](images/1-1-strategic-design.png)
- You can't apply tactical design in an effective way unless you begin with strategic design.
- Highlights **what is strategically important** to your business, **how to divide up the work** by importance, and **how to integrate** as needed.

### Key Concepts

- **_Bounded Contexts_**
  - A strategic design pattern for **segregating** domain models.
  - Within an explicitly _Bounded Context_, we develop a **_Ubiquitous Language_** as your **domain model**.
    - Important to engage with **_Domain Experts_** as you develop your model's _Ubiquitous Language_.
- **_Subdomains_** - Can help you deal with the **unbounded complexity of <u>legacy systems</u>**, and to improve your results on greenfield projects.
- **_Context Mapping_** - A technique to **integrate** multiple _Bounded Contexts_.

## Tactical Design (Low Level, Fine Detail)

![1-2-tactical-design](images/1-2-tactical-design.png)

- **_Aggregate_** pattern - Aggregate entities and value objects together into a **right-sized cluster**.
- **_Domain Events_** - Help you to **model explicitly** and to **share what has occurred within your model**.

# Chapter 2. Strategic Design with Bounded Contexts and the Ubiquitous Language

- DDD is primarily about **modeling** a _Ubiquitous Language_ in an explicitly _Bounded Context_.
- _Bounded Context_ is a **semantic contextual boundary**.
  - Components inside a _Bounded Context_ are **context specific**.
- When you are just **getting started**, your _Bounded Context_ is somewhat **conceptual** (think of it as part of your **_problem space_**).
- As your model starts to take on **deeper meaning** and **clarity**, your _Bounded Context_ will quickly transition to your **_solution space_**, with your model being **reflected as source code**.
- <u>What Is a Problem Space and a Solution Space?</u>
  - **Problem space:**
    - **High-level strategic analysis** and **DESIGN steps**.
    - Can use **simple diagrams** (e.g. **Context Maps**) as you discuss the high-level project drivers and note important **goals** and **risks**.
  - **Solution space:**
    - **IMPLEMENT** the solution.
    - Produce code that **supports integration with other _Bounded Contexts_**.
- **Model** inside the context boundary reflects a **language** (Ubiquitous Language) that is developed by the team working in the **_Bounded Context_**.

![1-1-strategic-design](images/1-1-strategic-design.png)

- **Boxes** inside the _Bounded Context_ represent the model, which may be implemented as **classes**.
- **_Core Domain_**
  - When the _Bounded Context_ is being developed as a **key strategic initiative** (killer feature).
  - **Choose wisely** what should be part of your Core Domain and what should not.
- Can think of **_Bounded Contexts_** as being **language boundaries**.
- <u>Bounded Contexts, Teams, and Source Code Repositories</u>
  - **Separate source code repository** for each _Bounded Context_.
  - One team could work on multiple _Bounded Contexts_, but **multiple teams should not work on a single _Bounded Context_**.
- **Other teams** would have a **different meaning for the same terminology**, because their business knowledge is within a **different context**.
- One **big reason** to use _Bounded Contexts_ is to solve a **common problem**:
  - Don't know **when to stop** piling more and more concepts into their domain models.
  - The language of the model becomes blurred.
  - Multiple languages in one large, confusing, unbounded model.
  - The product of trying to do too much, with too many people, in the wrong place.

## Domain Experts and Business Drivers

- There may be **hints** communicated by **business stakeholders** that could have been used to help the technical team make **better modeling choices**.
- **Department**, **team**, **business unit** or **divisions** can provide a **indication of where model boundaries should exist**.
- There is a trend toward grouping people **by project**.
  - Organized according to business drivers and under an **area of expertise**.

### Differences in Policies **by Function** (Example)

![2-1-context-specific-model](images/2-1-context-specific-model.png)

- Policy model:

  | Bounded context | Description                                                                                                                    |
  | --------------- | ------------------------------------------------------------------------------------------------------------------------------ |
  | Underwriting    | Expertise that is focused on underwriting, a policy is created based on the **evaluation of the risks** of the insured entity. |
  | Inspections     | Inspections area of expertise **inspecting a property** that is to be insured.                                                 |
  | Claims          | Claims area of expertise **tracks the request for payment** by the insured.                                                    |

- DDD emphasizes embracing such differences by **segregating** the different types into **different _Bounded Contexts_**.
- No need to name these UnderwritingPolicy, ClaimsPolicy, or InspectionsPolicy.

### Another Examples: What Is a Flight?

- In the **airline industry**, a "flight" can have **multiple meanings**:
  - A single takeoff and landing
  - Aircraft maintenance
  - Passenger ticketing
- Because each of these uses of "flight" is clearly **understood only by its context**, each should be modeled in a separate _Bounded Context_.

## [Problem] Case Study - Scrum-based agile project management application

- Unbounded model (Initial):

  ![2-2-unbounded-model](images/2-2-unbounded-model.png)

- Let's say we want to facilitate collaboration discussions within the **product team**.

  - Tenant, User, Permission models are needed to identify and authorize users.
  - Discussion represents one of the **collaborative tools** that we will support.

  ![2-3-unbounded-model](images/2-3-unbounded-model.png)

- Then, we decided that discussions belong within Forums and Discussions have Posts. Also we want to support Shared Calendars.

  ![2-4-unbounded-model](images/2-4-unbounded-model.png)

- And we need a way for **Tenants** to make **Payments**.

  - Will also sell tiered **support plans**, so we need a way to track support **incidences**.
  - Managed under an **Account**.

  ![2-5-unbounded-model](images/2-5-unbounded-model.png)

- And every product has a specific **Team** that works on the product.

  - Teams are composed of a single **Product Owner** and a number of **Team Members**.

  ![2-6-unbounded-model](images/2-6-unbounded-model.png)

- And shared calendars should not be limited to **bland** Calendar Entries.

  - Specific kinds of Calendar Entries, such as Reminders, Team Milestones, Planning and Retrospective Meetings, and Target Dates.

  ![2-7-unbounded-model](images/2-7-unbounded-model.png)

- The **LANGUAGE** is no longer purely about Scrum.
- For every named element, we might expect to have **two or three more** concepts to support those.

  ![2-8-unbounded-model](images/2-8-unbounded-model.png)

## Fundamental Strategic Design Needed

- Two fundamental strategic design tools:
  1. _Bounded Context_
     - \*Forces us to answer the question **"What is core?"**.
     - Should **hold closely all concepts** that are **core** to the strategic initiative.
  2. _Ubiquitous Language_
- **Note:** Concepts that survive the **stringent application of core-only filtering** are part of the _Ubiquitous Language_ of the team that owns the _Bounded Context_.

- How do we know **what is core?**

  - Have to bring together **two vital groups** of individuals into **one cohesive**, collaborative team: **_Domain Experts_** and **_software developers_**.
  - **Example:** In the domain of **Scrum**, count on the **_Domain Expert_** being a **Scrum Master** who thoroughly understands how Scrum is executed on a project.

  ![2-9-different-roles-in-ddd](images/2-9-different-roles-in-ddd.png)

- **Product Owner or Domain Expert?**
  - In some cases they **might be one** and the same.
  - This **doesn't mean** that the product owner is naturally an expert in the business's core competency.
- **_Domain Experts_**
  - Primarily focused on the business.
  - It's **their mental model** that we start with to **form the foundation** of the team's _Ubiquitous Language_.
- **_Developers_**
  - Need to carefully **resist the urge** to be so **technically centered**.
  - **Focus on Business Complexity, Not Technical Complexity**.
  - You are using DDD because the **business model complexity is high**.
  - Have to dig into the business model with **_Domain Experts_**.
- Should reject any tendency to allow documents to rule over conversation.
- The **best** Ubiquitous Language will be developed by a **collaborative feedback loop**.

## Challenge (Ask Questions) and Unify

- Question - What is core?
- Ask whether **each of the large-model concepts** adheres to the _Ubiquitous Language_ of Scrum.
- Models should **adhere to** the _Ubiquitous Language_ of Scrum.

  ![2-10-generic-model-names](images/2-10-generic-model-names.png)

  ![2-11-domain-driven-model-names](images/2-11-domain-driven-model-names.png)

- **Out of context** - Not part of the core Scrum language.

  ![2-12-out-of-context](images/2-12-out-of-context.png)

  ![2-13-out-of-context](images/2-13-out-of-context.png)

- **In context, but out of scope.** So, save it for later.

  - Calendar-based `Milestones`, `Retrospectives`, and the like.

  ![2-14-in-context-but-out-of-scope](images/2-14-in-context-but-out-of-scope.png)

- Assuming **threaded `Discussions`** will be part of the core model.

  - But, it requires a lot of **ancillary software component support**.
  - Hence, the full **Collaboration suite is out of context**.

  ![2-15-out-of-context](images/2-15-out-of-context.png)

- **Core Domain** - Essential model elements.

  - The model will **grow only as new concepts adhere to** the _Ubiquitous Language_ of Scrum.

  ![2-16-bounded-model](images/2-16-bounded-model.png)

## Developing a Ubiquitous Language (Model)

- **Don't limit** your _Core Domain_ to nouns alone.
  - Spoken language is composed of far more than nouns.
- But, when **constraining a Core Domain down to essential model**, we can focus on nouns.
- **Accelerate Your Discovery**
  - **Event Storming**
  - \***Concrete scenarios**
- Express your _Core Domain_ as a set of **concrete scenarios**.
  - Example (**Not a perfect example**, but it's a good start):
    - _Allow each backlog item to be committed to a sprint. The backlog item may be committed only if it is already scheduled for release. If it is already committed to a different sprint, it must be uncommitted first. When the commit completes, notify interested parties._
  - Describe how the very real software model components are used.
  - **Constraints** should also be part of the scenarios.
  - All about doing whatever is needed to **communicate well** on the team.
  - Be careful about the **time spent** in your domain-modeling efforts when it comes to **keeping documents**.
  - **Only do so as long as it is helpful** rather than burdensome.
- \*Ask the **WHO** question to clarify the initially stated scenario.
  - **Before** - _Allow each backlog item to be committed to a sprint..._
  - **After** - _The product owner commits each backlog item to a sprint..._
- In many cases, you should name each **persona** involved in the scenario and give some distinguishing attribute to other concepts such as to the backlog item and sprint.
- **Refined scenario:**
  - _The product owner commits a backlog item to a sprint. The backlog item may be committed only if it is already scheduled for release, and if a quorum of team members have approved commitment. If it is already committed to a different sprint, it must be uncommitted first. When the commitment completes, notify the sprint from which it was uncommitted and the sprint to which it is now committed._

### Putting Scenarios to Work (Executable Specs)

- \[Technique] **Specification by Example**, aka **Behavior-Driven Development (BDD)**.

  - It's to **collaboratively** develop and refine a _Ubiquitous Language_, model with a **shared understanding**, and determine whether your model **adheres to your specifications**.
  - By creating **acceptance tests**.
  - Restate the preceding scenario as an **executable specification**:

    ```
    Scenario: The product owner commits a backlog item to a sprint
      // Conditions
      Given a backlog item that is scheduled for release
      And the product owner of the backlog item
      And a sprint for commitment
      And a quorum of team approval for commitment
      // Action
      When the product owner commits the backlog item to the sprint
      // Result
      Then the backlog item is committed to the sprint
      And the backlog item committed event is created
    ```

  - To **validating** the domain model.
  - Work best to maintain the **document** form of the **scenario** associated with the **validation code** in **comments**.

### What about the Long Haul?

- The best learning, or knowledge acquisition, **take place over a long period of time**.
- It is a **mistake** for teams to take the view that innovation ends when maintenance begins.

## Architecture

- Hexagonal Architecture

  ![2-17-ports-and-adapters-architecture](images/2-17-ports-and-adapters-architecture.png)

- Common **layers** in a _Bounded Context_:

  1. **_Input Adapters_** - User interface controllers, REST endpoints, and message listeners (subscribers)
  2. **_Application Services_** - Orchestrate use cases, manage transactions.
  3. \***_Domain model_** (Core)
  4. **_Output Adapters_** - Persistence management, message senders (publishers)

  ![2-18-ports-and-adapters-architecture](images/2-18-ports-and-adapters-architecture.png)

- **Domain model** should be **free of technology**.
  - That's why **transactions** are managed by the **application services**.
- \***Ports and Adapters** can be used as a **foundational architecture** (basis).
- Architectures that can be used with DDD:
  - Event-Driven Architecture - Event Sourcing, Domain Events.
  - CQRS
  - Reactive and Actor Model
  - REST
  - SOA
  - \***Microservices** - Essentially equivalent to DDD **_Bounded Contexts_**.
  - Cloud computing
- Some consider a microservice to be much smaller than a DDD _Bounded Context_.
  - **Example:** Both the **Product microservice** and the **BacklogItem microservice** will still be **in the same** larger, logical **_Bounded Context_**.

# Chapter 3.Strategic Design with Subdomains

- The **most optimal** modeling composition: one _Subdomain_ per _Bounded Context_, and one _Bounded Context_ per _Subdomain_.

## What Is a Subdomain?

- **Sub-part** of your overall business domain.
- A **single, logical** domain model.
- **Clear** area of expertise.

## Types of Subdomains

![3-1-types-of-subdomains](images/3-1-types-of-subdomains.png)

1. **_Core Domain_**
   - This is where you **invest significant resources**.
   - Since an organization can't be excellent in everything, _Core Domain_ **defines where it must excel**.
2. **_Supporting Subdomain_**
   - **Custom development** is required as **no off-the-shell solution** exists.
   - Could consider outsourcing this kind of _Bounded Context_.
3. **_Generic Subdomain_**
   - May be available for purchase **off-the-shelf**.
   - May be outsourced.
   - Developed in house by a team that doesn't have the kind of elite developers.

## Dealing with Complexity

- **Sources** of complexity:
  - **Legacy systems**
  - Systems purchased through software licensing
- Need to reason about them when they have an impact on your _Core Domain_ project.
- **Unbounded legacy systems**
  - **Opposed to** the DDD way of designing with _Bounded Contexts_.
  - Many logical domain models exist inside one legacy system.
- Can use **_Subdomains_** to **identify** each logical domain models (marked off by a dashed box).

  - We **imagine** having separate _Ubiquitous Languages_ so we can understand **how to integrate with it**.
  - This way we can determine the _Subdomains_ that are **more valuable** to the business and necessary for our project.

  ![3-2-unbounded-model-with-logical-subdomains](images/3-2-unbounded-model-with-logical-subdomains.png)

- If you must create a **second model in the same _Bounded Context_ (within _Core Domain_)**, you should **segregate it** using a **separate Module** as a **supporting subdomain**.

# Chapter 4. Strategic Design with Context Mapping

- **_Context Mapping_** - To integrate _Bounded Contexts_.
- E.g. _Collaboration Context_ is the **source** of the `Discussion`, and the _Agile Project Management Context_ is the **consumer** of the `Discussion`.

  ![4-1-context-mapping](images/4-1-context-mapping.png)

- The mapping line represents the **translation** that exists between the **two languages**.
- Either the teams would need an **interpreter**, or have to **learn about the other's language**.
- \*There are several kinds of **inter-team relationship** and **integration**.

## Kinds of Mappings

### 1. Partnership (in the same boat, highly interdependent)

![4-2-partnership](images/4-2-partnership.png)

- Align the two teams with a **dependent set of goals**.
- Two teams will succeed or fail **together**.
- **High commitment** required from both teams.
- Can be **challenging to maintain** over the **long term**.
- Best to **set limits** on the term of the relationship.

### 2. Shared Kernel

![4-3-shared-kernel](images/4-3-shared-kernel.png)

- **Share** a small but **common model**.
- **Only one team** (clear ownership) will maintain the code, build, and test for what is shared.
- Often **very difficult** to conceive and maintain.
  - Require **constant agreement** on what constitutes the model to be shared.
- Feasible if all involved agreed that the **kernel is better than going _Separate Ways_**.

### \*3. Customer-Supplier (Typical, Practical)

![4-4-customer-supplier](images/4-4-customer-supplier.png)

- It's up to the _Customer_ to plan with the _Supplier_ to meet various expectations.
- **_Supplier_ determines** what the _Customer_ will get and when.
- A very typical and practical relationship between teams.

### 3.1. \[Downstream] Conformist

![4-5-conformist](images/4-5-conformist.png)

- Downstream team **can't sustain** an effort to translate the Ubiquitous Language of the upstream model.
- E.g. Consider the need to conform to the Amazon.com model when integrating as one of Amazon's affiliate sellers.

### 3.2. \[Downstream] Anticorruption Layer (Translation)

![4-6-anticorruption-layer](images/4-6-anticorruption-layer.png)

- The **most defensive** _Context Mapping_ relationship, where the downstream team creates a **translation layer**.
- **Whenever possible**, you should create an _Anticorruption Layer_, so you can produce model concepts that specifically fit your business needs and keep you **isolated from foreign concepts**.
- The **cost** of the translation layer can be **high**.

### 3.3. \[Upstream] Open Host Service (API)

![4-7-open-host-service](images/4-7-open-host-service.png)

- Defines a **interface** (API) that gives access to your _Bounded Context_ **as a set of services**.
- If you were Team 2 and could not take time to create an isolating _Anticorruption Layer_, it would be much more **tolerable** to be a **Conformist**.

### 3.4. \[Upstream] Published Language (Content Type)

![4-8-published-language](images/4-8-published-language.png)

- Consumers can translate from and into the **shared language** (contract).
- E.g. XML, JSON, Protobuf, Avro
- Use in conjunction with _Open Host Service_.

### 4. Separate Ways

![4-9-separate-ways](images/4-9-separate-ways.png)

- Describes a **situation** where the functionality that you seek is **not fully provided by any** one Ubiquitous Language.
- In this case **produce your own** specialized solution in your _Bounded Context_.

### Big Ball of Mud

- Serious problems you will experience when you must work in or integrate with one.
  1. A growing number of _Aggregates_ **cross-contaminate** because of **unwarranted connections and dependencies**.
  2. Maintaining one part of the _Big Ball of Mud_ **causes ripples** across the model.
- If you must integrate with one, create an **_Anticorruption Layer_**.

  ![4-10-big-ball-of-mud-integration](images/4-10-big-ball-of-mud-integration.png)

- \*Whatever you do, **don't speak that language!**

## Making Good Use of Context Mapping

- The **least favorable** situations - Use **database** or **file system integration**.
- Three **integration types**:
  - Messaging (**most robust**) > RESTful HTTP > RPC with SOAP (**least robust**)

### 1. RPC with SOAP (Synchronous)

![4-11-rpc-with-soap](images/4-11-rpc-with-soap.png)

- To make using services from another system look like a simple **method invocation**.
- Potential problems - Network failure, latency
- **Strong coupling** between a client _Bounded Context_ (downstream) and the _Bounded Context_ providing the service (upstream).
- Lack robustness.
- Your client _Bounded Context_ can be designed with an _Anticorruption Layer_ to **isolate** your model **from unwanted outside influences**.

### 2. RESTful HTTP (Synchronous)

![4-12-restful-http](images/4-12-restful-http.png)

- A **common mistake** - Design resources that **directly reflect** the _Aggregates_ in the domain model.
- \*Resources should be designed to **follow client-driven use cases**.
  - What the client needs is what drives the design of the resources, and not the model's current composition.

### 3. Messaging (Asynchronous)

![4-13-messaging](images/4-13-messaging.png)

- One of the **most robust** forms of integration.
- **Going Asynchronous with REST** - Using REST-based **polling** of a sequentially growing set of resources (e.g. _Domain Events_).
- **_Aggregate_** in one Bounded Context **PUBLISHES a _Domain Event_**, which could be consumed by **any number** of interested parties.
- **Are Domain Event CONSUMERS Conformists?**
  - Should **not use** the event types (e.g. **classes**) of an event publisher.
  - Should depend only on the **schema of the events** (_Published Language_).
- Sometimes, however, a client Bounded Context will need to **proactively SEND a _Command Message_** to a service Bounded Context to force some action.
- The quality of the overall solution will **depend heavily** on the quality of the chosen messaging mechanism.
  - Basically, the messaging mechanism should support **_At-Least-Once Delivery_**.
- **Subscribing** _Bounded Context_ must be implemented as an **_Idempotent Receiver_** because it is possible for the message to be **delivered more than once**.
  - \***Idempotency** (preferred) - Safely reapplies the operation with the exact same results that the previous delivery caused (no tracking required).
  - **De-duplication** - Ignores the repeated message by tracking the message ID.

## An Example in Context Mapping

- Three different Policy types in three different _Bounded Contexts_.

  ![4-14-three-different-policy-types](images/4-14-three-different-policy-types.png)

- **Where** does the "policy of record" live?
  - Belong to the **underwriting** division since that is where it **originates** (source).
- **Query-Back** - If there is a need **for more Policy data** than the `PolicyIssued` _Domain Event_ provided, the **subscribing** _Bounded Context_ can **query** the _Underwriting Context_.

  - **Cons** - More network round trips.

  ![4-15-query-back](images/4-15-query-back.png)

- **Enrichment** - Enriching Domain Events with data to satisfy the needs of all consumers.
- **Enrichment versus Query-Back Trade-offs**
  - Enrichment = Greater autonomy
    - **But**, difficult to predict the data that all consumers need.
    - Too much enrichment can lead to **poor security**.
