# JELLOG Documentation

JELLOG Framework offers an **opinionated architecture** to build enterprise software solutions with **best practices** on top of the **.NET** and the **ASP.NET Core** platforms. It provides the fundamental infrastructure, production-ready startup templates, modules, themes, tooling, guides and documentation to implement that architecture properly and **automate the details** and repetitive works as much as possible.

## Getting Started

* [Quick Start](Tutorials/Todo/Overall.md) is a single-part, quick-start tutorial to build a simple application with the JELLOG Framework. Start with this tutorial if you want to quickly understand how JELLOG works.
* [Getting Started](Getting-Started.md) guide can be used to create and run JELLOG based solutions with different options and details.
* [Web Application Development Tutorial](Tutorials/Part-1.md) is a complete tutorial to develop a full stack web application with all aspects of a real-life solution.

### UI Framework Options

JELLOG Framework can work with any UI framework, while the following frameworks are supported out of the box:

<img width="500" src="images/ui-options.png">

### Database Provider Options

JELLOG Framework can work with any database provider, while the following providers are supported out of the box:

<img width="500" src="images/db-options.png">

## Exploring the Documentation

JELLOG has a **comprehensive documentation** that not only explains the JELLOG Framework, but also includes **guides** and **samples** to help you on creating a **maintainable solution** by introducing and discussing common **software development principle and best practices**.

### Architecture

JELLOG offers a complete, modular and layered software architecture based on [Domain Driven Design](Domain-Driven-Design.md) principles and patterns. It also provides the necessary infrastructure to implement this architecture.

* See the [Modularity](Module-Development-Basics.md) document to understand the module system.
* [Implementing Domain Driven Design book](https://jellog.io/books/implementing-domain-driven-design?ref=doc) is an ultimate guide for who want to understand and implement the DDD with the JELLOG Framework.
* [Microservice Architecture](Microservice-Architecture.md) document explains how JELLOG helps to create a microservice solution.
* [Multi-Tenancy](Multi-Tenancy.md) document introduces multi-tenancy and explores the JELLOG multi-tenancy infrastructure.

### Infrastructure

There are a lot of features provided by the JELLOG Framework to achieve real world scenarios easier, like [Event Bus](Event-Bus.md), [Background Job System](Background-Jobs.md), [Audit Logging](Audit-Logging.md), [BLOB Storing](Blob-Storing.md), [Data Seeding](Data-Seeding.md), [Data Filtering](Data-Filtering.md).

### Cross Cutting Concerns

JELLOG also simplifies (and even automates wherever possible) cross cutting concerns and common non-functional requirements like [Exception Handling](Exception-Handling.md), [Validation](Validation.md), [Authorization](Authorization.md), [Localization](Localization.md), [Caching](Caching.md), [Dependency Injection](Dependency-Injection.md), [Setting Management](Settings.md), etc. 

### Application Modules

Application Modules provides pre-built application functionalities;

* [**Account**](Modules/Account.md): Provides UI for the account management and allows user to login/register to the application.
* **[Identity](Modules/Identity.md)**: Manages organization units, roles, users and their permissions, based on the Microsoft Identity library.
* [**IdentityServer**](Modules/IdentityServer.md): Integrates to IdentityServer4.
* [**Tenant Management**](Modules/Tenant-Management.md): Manages tenants for a [multi-tenant](Multi-Tenancy.md) (SaaS) application.

See the [Application Modules](Modules/Index.md) document for all pre-built modules.

### Startup Templates

The [Startup templates](Startup-Templates/Index.md) are pre-built Visual Studio solution templates. You can create your own solution based on these templates to **immediately start your development**.

