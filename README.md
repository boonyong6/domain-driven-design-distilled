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
