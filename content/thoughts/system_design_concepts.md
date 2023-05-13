---
title: "Key Design Concepts"
date: 2023-05-13T21:09:14+04:00
tags: ['engineering', 'system design', 'development']
---

In this article, I am going to go through the key software design concepts and considerations that are preferred or sometimes required in the modern software development environment.

<!--more-->

# Table of content
- [CQRS](#cqrs)
- [API Gateway](#api-gateway)
- [Strangler](#strangler)
- [Circuit Breaker](#circuit-breaker)
- [Ambassador](#ambassador)
- [Sharding](#sharding)
- [Microservice architecture](#microservice-architecture)
- [Event sourcing](#event-sourcing)

---
## CQRS

#### What?

CQRS is a pattern for separating command (writing) from request (reading) processing. Traditional application architecture uses the same data model to handle both commands and queries, which can cause performance, scalability and complexity issues. CQRS overcomes this problem with separate command and query models and data stores.

The CQRS architecture uses separate writing and reading models for commands and queries, respectively. Each model has different data stores to suit its specific application. Commands are used to change the state of the application. Queries are used to get data from the application.

#### Why?

- Performance.
  Decoupling the read and write model enables more efficient queries and more optimized data storage for reads.
  This can result in significant performance gains, especially for read-intensive applications.

- Scalability.
  By separating the read model from the write model, it becomes easier to scale each model independently of the other, allowing for greater scalability of the application as a whole.

- Complexity.
  By simplifying the data model and reducing the number of dependencies between components, separating the read and write models can reduce the complexity of the application.

#### How?

- Identify use cases.
  Determine the use cases in which CQRS can provide the most value. These will typically be applications with complex query requirements or high volumes of reads.

- Separate the models.
  Using different data stores optimised for their specific use cases, create separate models for handling commands and queries.

- Define the API.
  Define the API for both the read and write models, ensuring that the API is consistent and easy to use.

- Test thoroughly.
  Thoroughly test the CQRS architecture to ensure that it works as expected and that it meets the requirements for security and performance.

#### Cons?

- Increased complexity.
  Implementing CQRS can increase application architecture complexity, potentially making debugging and troubleshooting more difficult.

- Higher development costs.
  Implementation of CQRS requires additional development effort for model separation and API definition.

- Learning curve.
  CQRS is a new and complex architectural model that may require a significant learning curve for programmers.

- Potential consistency issues.
  As the read model is separate from the write model, there is a potential for consistency issues if changes to the write model are not propagated to the read model in a timely manner.

---

## API Gateway

#### What?

An API Gateway is a software layer that connects backend services and client applications.
It acts as a reverse proxy, routing requests and handling tasks like authentication, rate limiting, and caching.

#### Why?

- Access simplification.
  Client applications often need to access multiple backend services, each with their own API.
  By providing a single entry point for accessing all services, the API Gateway simplifies the development process for client applications.

- Application evolution.
  The API Gateway enables backend services to evolve independently over time, without disrupting client applications, by facilitating seamless integration of changes to APIs or addition of new services.

- Auth^2 (Authentication/Authorization).
  The API Gateway manages authentication and authorization for client requests, making the authentication process for client applications more streamlined and efficient.

- Caching.
  API Gateway can take responsibility for caching request's data, therefore bringing greater perfomance for clients, less load to applications, reduced costs for infrastructure.

- Payload transformations
  Certain API Gateway implementations allow developers to manipulate both payloads and responses, eliminating unnecessary complications.

- Monitoring.
  API Gateways offer monitoring and analytics features that empower developers to gain valuable insights into their services' usage patterns, enabling them to identify areas for optimization and make data-driven decisions.

#### How?

- Identify services to be exposed.
  Determine which backend services will be exposed through the API Gateway, taking into account security and performance considerations.
- Define API.
  Define APIs for each backend service, including endpoints, parameters, and data formats.
- Select and configure gateway.
  There are various implementations of gateways, both standalone (Kong, Krakend, Apigee) and propietary(AWS APIGW, GCP Gateway). Choose depending on the environment you have.
  Configure the API Gateway to route requests to the appropriate backend services, handle authentication and authorization, and implement other required features such as rate limiting and caching.
- Test and deploy.
  Test the API Gateway thoroughly before deploying it to production, ensuring that it is performing as expected and is meeting security and performance requirements.
- Monitor and iterate.
  Monitor the API Gateway in production, using analytics to identify areas for optimization and iterating on the configuration as needed.

#### Cons?

- Increased complexity.
  Adding another layer to the application infrastructure can increase complexity and potentially make debugging and troubleshooting more difficult.
- Single point of failure.
  If not configured for high availability, the API gateway can become a single point of failure.
- Performance overhead.
  The API Gateway introduces additional network hops and processing overhead, which can have an impact on performance.
- Cost.
  Especially for large deployments, API gateway services can be expensive.

---

## Strangler

#### What?

The Strangler Pattern is a software development technique that involves incrementally replacing an existing application with a new one by gradually diverting traffic from the old application to the new one. The term "Strangler" comes from the analogy of a strangler vine that slowly envelops and replaces a tree over time.

#### Why?

- Legacy applications can be difficult to maintain and evolve due to their age and complexity.
  By gradually replacing the application's functionality, the Strangler Pattern allows developers to modernize the application while minimizing the risks and costs associated with a complete rewrite.

- Strangler allows for incremental delivery of new features and functionality.
  This means that developers can deliver new features and functionality to users while still maintaining the existing application.

- Strangler allows developers to test new functionality in a controlled environment before releasing it to users.
  This helps to minimize the risk of introducing bugs and other issues that could impact users.

#### How?
1. Identify the functionality that needs to be replaced in the legacy application.
1. Build a new application that provides the same functionality as the legacy application.
1. Divert traffic from the legacy application to the new application in a controlled manner.
   This can be done by gradually redirecting users to the new application, or by using a proxy that intercepts requests and redirects them to the new application.
1. Monitor the traffic to ensure that the new application is performing as expected and that there are no issues with the transition.
1. Gradually replace more and more functionality in the legacy application with the new application until the legacy application is no longer needed.

#### Cons?
- It can be complex and time consuming to implement.
- It may introduce complex application architecture if done wrong. The cost will increase exponentially.
- It may result in long adoption. Until then, both old and new applications will have to be in place. This can increase maintenance cost.

---

## Circuit Breaker
`TODO`

---

## Ambassador
`TODO`

---

## Sharding
`TODO`

---

## Microservice architecture
`TODO`

---

## Event sourcing
`TODO`