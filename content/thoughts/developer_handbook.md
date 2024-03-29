---
title: "Developer handbook"
date: 2023-05-13T18:00:00+04:00
tags: ['engineering', 'manual', 'development', 'best-practice']
---

# Introduction

Developing software is not just about writing code.
It is about creating a high-quality product solution that satisfies the needs of the customer while being maintainable, scalable, and efficient.
In order to achieve this goal, it is important to follow best practices that have been developed over years of experience in the industry.

In addition to the technical aspects of software development, it's important to consider the human aspect as well. A key factor in the success of a software development team is how well new developers are onboarded and integrated into the team's culture and practices. By providing a clear and simple onboarding process, new team members can quickly become productive and contribute to the success of the project.

<!--more-->

# Code management practices

Version control is an essential tool for managing code in any software project. Git is a popular and powerful version control system used by many developers and organizations.

## Basics

Use branches to isolate changes and avoid conflicts.
  A branch is a separate line of development that allows you to work on a feature or bug fix without affecting the main codebase.

Name branches clearly and consistently.
Use a naming convention that describes the purpose of the branch and makes it easy to identify.
Always refer the task in the name, it will be much easier to track the origins of the change.
For example, `feature/FC-123-add-loan-management` or `bugfix/fix-loan-controller`.
Use variety of of branch tags to reflect the context of the change: `feature`,`bugfix`,`hotfix`,`refactoring`.

Write descriptive and meaningful commit messages. A commit message should explain what changes were made and why they were necessary. It's important to provide context and avoid ambiguity.

Keep the commit history clean and concise.
Using rebase and squash in Git is a better practice than dealing with merge commits because it helps maintain a cleaner, more linear history. By squashing or combining related commits into one, the commit history is simplified and easier to follow.

Additionally, rebasing helps keep the codebase up-to-date with the latest changes from the upstream branch. This makes it easier to resolve conflicts and avoids creating unnecessary merge commits that can clutter the commit history. In short, using rebase and squash in Git can lead to a cleaner, more organized, and easier to maintain codebase.

 Example of repository that utilises merge commits which branch off different versions of masters.

  ```yaml
  * 0a1b2c3 (HEAD -> feature1) Merge branch 'master' into feature1
  |\
  | * 6d7e8f9 (origin/master, master) Add new feature A
  | | * 2b3c4d5 (feature2) Merge branch 'master' into feature2
  | | |\
  | | | * 4e5f6g7 Add new feature B
  | | |/
  | |/|
  | * | 8h9i0j1 Add bugfix C
  | |/
  | * 1k2l3m4 Add new feature D
  |/
  * 5n6o7p8 Initial commit
  ```

Example of repository that utilises squash style of merging

```yaml
* dcb5b76 (HEAD -> feature/new-feature) Commit message for squashed and rebased commits
* a5f84a9 Commit message for squashed and rebased commits
* 2c4a1d3 Commit message for squashed and rebased commits
* 90c5d08 Commit message for squashed and rebased commits
* e2f3c18 (master) Commit message on master
* 8f3da7f Commit message for squashed and rebased commits
* 7a482e5 Commit message for squashed and rebased commits
* 1346e22 Commit message for squashed and rebased commits
* 2d6c1f1 Commit message for squashed and rebased commits
```


## Github flow

- Way to follow GithubFlow
    - Create a new branch: Create a new branch from the main branch that you are working on.
    - Add commits: Add commits to the branch as you work on the feature or bug fix. It's important to commit early and often.
    - Open a pull request: Once you have completed your work and pushed your commits to the branch, open a pull request (PR) against the main branch.
    - Review and discuss: Your team members can now review your changes, add comments, and request changes if necessary. You can also discuss any issues or questions that come up during the review process.
    - Merge the pull request: Once the changes have been reviewed and approved, you can merge the PR into the main branch. This will incorporate your changes into the codebase and make them available to everyone.
    - Deploy: With GitHub Flow, deploying your changes is integrated into the process. Once the changes are merged into the main branch, they can be deployed to production.

## Referrals

- [GithubFlow Specification](https://docs.github.com/en/get-started/quickstart/github-flow)
- [Branch naming conventions](https://www.scaler.com/topics/git/git-branch-naming-conventions/)

# Structuring conventions

It is important to separate different concerns and modules properly. One of the common approaches is to divide the application into several major parts, such as API, LIB, and WORKER.

**Api**

The API section should contain everything that is related to the API, such as controllers, serializers, and routes. It is important to keep this section separate from the rest of the application, as it is often the entry point for external requests.

**Core**

The CORE section should contain everything that is related to business logic, such as models, services, and repositories. This section should be further divided into subdirectories based on domain entities. For example, an e-commerce application could have subdirectories for products, orders, and customers. Inside each subdirectory, it is recommended to further separate the functionality into actions, such as create, update, and delete.

**Lib**

The LIB directory, also known as the library directory. While the CORE directory contains the business logic functionality of the application, there are often other components that are required for this logic to work, such as third-party libraries or custom classes.

By separating these components into the LIB directory, we can ensure that they are organized and easily accessible, while also keeping the business logic directory focused on the core functionality of the application.

**Worker**

The WORKER section should contain everything that is related to background processing and event handling, such as background jobs and event listeners. This section should also be further divided into subdirectories based on domain entities or functional categories.

## Examples

```ruby
app/
  api/
    controllers/
      products_controller.rb
      orders_controller.rb
      customers_controller.rb
    serializers/
      product_serializer.rb
      order_serializer.rb
      customer_serializer.rb
    routes.rb
  core/
    products/
			steps/
				find_product.rb
      create.rb
      update.rb
      delete.rb
      product.rb
    orders/
      create.rb
      update.rb
      delete.rb
      order.rb
    customers/
      create.rb
      update.rb
      delete.rb
      customer.rb
	lib/
		resources/
			order_repository.rb
			event_publisher.rb
    common/
      technical.rb
      not_related_to_business_logic.rb
  worker/
    orders/
      process_order.rb
    events/
      send_email_on_signup.rb
```

## Referrals
- [Domain directory structure](https://betterprogramming.pub/divide-code-by-domains-and-features-and-keep-it-scalable-bb5bd66cf3d2)

# Naming conventions

Naming conventions play a crucial role in the overall readability and maintainability of your code. Therefore, it is important to follow some standard conventions when naming your entities.

One such convention is the A/HC/LC pattern, which stands for Abbreviation, High context, and Low context.

The convention provides a structure for naming entities based on their level of abstraction, making it easier for developers to understand the intent of the code.

| Name | Prefix | Action (A) | High context (HC) | Low context (LC) |
| --- | --- | --- | --- | --- |
| getUser |  | get | User |  |
| getUserMessages |  | get | User | Messages |
| handleClickOutside |  | handle | Click | Outside |
| shouldDisplayMessage | should | Display | Message |  |

## Referrals

- [A/HC/LC convention](https://github.com/kettanaito/naming-cheatsheet)

# Qualitative API documentation

API documentation is crucial for the development process and maintenance of the project. It provides a clear description of all available endpoints, their parameters, response codes, and data models. OpenAPI is a widely used standard for documenting APIs that helps developers understand and utilize your API.

To properly document your API using OpenAPI, you should follow these guidelines:

1. Define clear and concise descriptions for each endpoint. Make sure to include all required parameters, their data types, and their descriptions.
2. Organize your API documentation into sections based on functionality or resource type.
3. Provide examples for requests and responses. This can help developers understand the expected behavior of your API.
4. Define response codes and their descriptions. This will help developers understand how to handle errors and other unexpected behavior.
5. Use the correct HTTP methods for each endpoint.
6. Use the appropriate data types for each parameter.
7. Define data models for each response. This can help developers understand the structure and content of the response.
8. Use the appropriate data formats for each parameter and response.
9. Automate the generation of your API documentation. Tools like Swagger UI and ReDoc can help simplify this process and make it easier for developers to interact with your API.

Properly documenting your API using OpenAPI can improve the quality of your product in several ways.

- It can help developers understand the expected behavior of your API, which can reduce the likelihood of errors and improve overall reliability.
- It can also make it easier for new developers to onboard and contribute to your project, which can improve the speed and efficiency of development.
- Additionally, clear and concise API documentation can improve the overall user experience of your product by making it easier for developers to integrate with your API.

## Examples

```yaml
openapi: 3.0.0
info:
  version: 1.0.0
  title: Example API

paths:
  /users:
    post:
      summary: Create a new user
      operationId: createUser
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/UserCreateRequest'
      responses:
        '201':
          description: Created
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/UserCreateResponse'
        '400':
          description: Bad Request
        '500':
          description: Internal Server Error

components:
  schemas:
    UserCreateRequest:
      type: object
      properties:
        name:
          type: string
        email:
          type: string
        password:
          type: string
      required:
        - name
        - email
        - password
    UserCreateResponse:
      type: object
      properties:
        id:
          type: integer
        name:
          type: string
        email:
          type: string
        created_at:
          type: string
          format: date-time
        updated_at:
          type: string
          format: date-time
      required:
        - id
        - name
        - email
        - created_at
        - updated_at
```

## Referrals

- [OpenAPI Specification](https://spec.openapis.org/oas/v3.1.0)
- [OpenAPI Tooling](https://openapi.tools/)
- [Stoplight API Management system](https://stoplight.io/)

# Architectural principles

## SOLID

This stands for Single Responsibility, Open-Closed, Liskov Substitution, Interface Segregation, and Dependency Inversion.

### Single Responsibility Principle (SRP)

Each class or module should have only one responsibility, which should be encapsulated within that unit. This helps to avoid "God classes" and makes your code more modular and flexible.

```ruby
# BAD: A class that violates SRP
class User
  def initialize(name, email)
    @name = name
    @email = email
  end

  def send_email(subject, message)
    # Sends email using the user's email address
  end

  def log_in(password)
    # Logs the user in
  end
end

# GOOD: A class that follows SRP
class User
  def initialize(name, email)
    @name = name
    @email = email
  end

  def name
    @name
  end

  def email
    @email
  end
end

class EmailSender
  def send_email(to, subject, message)
    # Sends an email to the given recipient
  end
end

class Authenticator
  def log_in(user, password)
    # Authenticates the user with the given password
  end
end
```

### Open-Closed Principle (OCP)

Your code should be open for extension but closed for modification. This means that you should be able to add new functionality to your application without modifying existing code, which helps to reduce the risk of introducing bugs.

```ruby
# BAD: A class that violates OCP
class Order
  def initialize(items)
    @items = items
  end

  def calculate_total
    total = 0
    @items.each do |item|
      total += item.price
    end
    total
  end
end

# GOOD: A class that follows OCP
class Order
  def initialize(items)
    @items = items
  end

  def calculate_total
    calculator = Calculator.new(@items)
    calculator.calculate
  end
end

class Calculator
  def initialize(items)
    @items = items
  end

  def calculate
    total = 0
    @items.each do |item|
      total += item.price
    end
    total
  end
end

class DiscountCalculator < Calculator
  def calculate
    total = super
    if @items.size > 10
      total -= 100
    end
    total
  end
end
```

### Liskov Substitution Principle (LSP)

Subtypes should be substitutable for their base types without affecting the correctness of the program. This means that you should be able to use a subclass wherever the superclass is expected, without causing unexpected behavior.

```ruby
# BAD: A class hierarchy that violates LSP
class Rectangle
  attr_accessor :width, :height
  def area
    @width * @height
  end
end

class Square < Rectangle
  def width=(value)
    @width = value
    @height = value
  end

  def height=(value)
    @height = value
    @width = value
  end
end

# GOOD: A class hierarchy that follows LSP
class Shape
  attr_accessor :width, :height
  def area
    raise NotImplementedError
  end
end

class Rectangle < Shape
  def area
    @width * @height
  end
end

class Square < Shape
  def width=(value)
    @width = value
    @height = value
  end

  def height=(value)
    @height = value
    @width = value
  end

  def area
    @width * @height
  end
end
```

### Interface Segregation Principle (ISP)

Clients should not be forced to depend on interfaces they do not use. This means that you should split large interfaces into smaller, more focused ones to avoid unnecessary dependencies.

```ruby
# BAD: A class that violates ISP
class Animal
  def speak
    raise NotImplementedError
  end

  def fly
    raise NotImplementedError
  end
end

class Dog < Animal
  def speak
    puts "Bark!"
  end

  def fly
    # This method should not be implemented by a dog
  end
end

# GOOD: A class that follows ISP
class Animal
  def speak
    raise NotImplementedError
  end
end

class FlyingAnimal < Animal
  def fly
    raise NotImplementedError
  end
end

class Dog < Animal
  def speak
    puts "Bark!"
  end
end

class Bird < FlyingAnimal
  def fly
    puts "Flap, flap, flap!"
  end
end
```

### Dependency Inversion Principle (DIP)

High-level modules should not depend on low-level modules. Both should depend on abstractions. This means that you should depend on abstractions (interfaces) instead of concrete implementations, which makes your code more flexible and easier to test.

```ruby
# BAD: A class that violates DIP
class UserService
  def initialize
    @repository = UserRepository.new
  end

  def create_user(name, email)
    user = User.new(name, email)
    @repository.save(user)
  end
end

class UserRepository
  def save(user)
    # save the user to a database
  end
end

# GOOD: A class that follows DIP
class UserService
  def initialize(repository)
    @repository = repository
  end

  def create_user(name, email)
    user = User.new(name, email)
    @repository.save(user)
  end
end

class UserRepository
  def save(user)
    # save the user to a database
  end
end

repository = UserRepository.new
service = UserService.new(repository)

service.create_user("John", "john@example.com")
```

## DRY

This stands for Don't Repeat Yourself. This principle encourages you to avoid duplicating code by creating reusable functions or modules. Some rules and practices that follow DRY principles are:

- Extracting common functionality into shared modules or libraries to avoid duplication.
- Using helper functions or utility classes to encapsulate common operations.
- Refactoring code to remove duplication and increase reuse.

## KISS

This stands for Keep It Simple, Stupid. This principle encourages you to write simple, clear, and easy-to-understand code. Some rules and practices that follow KISS principles are:

- Writing code that is easy to read and understand.
- Avoiding unnecessary complexity, such as over-engineering or premature optimization.
- Using simple and straightforward algorithms and data structures.

## Referrals

- [KISS Definition](https://people.apache.org/~fhanik/kiss.html)
- [DRY Definition](https://www.plutora.com/blog/understanding-the-dry-dont-repeat-yourself-principle)
- [SOLID Definition](https://www.freecodecamp.org/news/solid-design-principles-in-software-development/)

# Architectural patterns

## Transactional outbox

### What is outbox?
The Transactional Outbox Pattern is an architectural pattern for ensuring reliable and atomic message delivery in distributed systems. It offers the possibility of decoupling the sending of messages from the transaction limit of the main business process, thus improving system reliability and performance.

The transactional outbox pattern involves capturing messages that need to be sent as part of a transactional operation and storing them in an outbox table within the same database transaction. These messages are then asynchronously processed and sent to external systems using a background process or messaging infrastructure. The outbox acts as a buffer that guarantees the eventual delivery of messages, even if the main transaction fails or is rolled back.

### Constraints of implementing outbox
To successfully apply the transactional outbox pattern, the following constraints should be met:

- **Atomicity**
  The messages in the outbox should be stored and processed within the same transaction as the main business operation to maintain atomicity.
- **Durability**
  The outbox messages should be persisted reliably to ensure that they are not lost in case of system failures.
- **Reliability**
  The background process or messaging infrastructure responsible for processing the outbox messages should guarantee eventual delivery and handle failures gracefully.
- **Idempotency**
  The processing of outbox messages should be idempotent to handle potential duplicates or retries without causing unintended side effects.

```ruby
# OutboxJob model represents a message in the outbox table
class OutboxJob < ApplicationRecord
  # Fields: id, payload, destination, metadata, created_at, updated_at
end

# Service responsible for handling outbox messages
class OutboxService
  def self.enqueue(payload, destination, metadata = {})
    OutboxMessage.create!(payload: payload, destination: destination, metadata: metadata)
  end

  def self.process_outbox
    OutboxMessage.transaction do
      messages = OutboxMessage.lock.where(processed_at: nil).order(:created_at)

      messages.each do |message|
        send_message(message)
        message.update!(processed_at: Time.now)
      end
    end
  end

  private

  def self.send_message(message)
    # Send the message to the destination using an appropriate method
    # Example: HTTP request, publish to a message queue, etc.
    puts "Sending message: #{message.payload} to #{message.destination}"
  end
end

# Usage example
class OrderService
  def create_order(params)
    Order.transaction do
      order = Order.create!(params)
      OutboxService.enqueue(order.to_json, '/orders')
    end
  end
end
```
## Async job
### What is async job?
The asynchronous job model, also known as asynchronous processing or background jobs, offloads time-intensive or non-blocking tasks for asynchronous processing.
The system queues these jobs for later processing, rather than performing them synchronously within the request-response cycle.
This pattern allows the application to respond quickly to user requests and delegate resource-intensive or slow operations to separate worker processes or background job queues.
### How to use it effectively?
The async job pattern is particularly useful in scenarios where tasks can be performed asynchronously without affecting the immediate user experience. It is beneficial in the following situations:

- Processing tasks that require significant time or computational resources, such as generating reports, large data imports/exports, image processing, or intensive calculations.
- Performing tasks that involve external services or APIs, such as sending emails, processing payments, or integrating with third-party systems.
- Executing tasks that can be deferred or processed in the background, such as data synchronization, notifications, or cache invalidation.
## Dependency management
### What is DM?

Managing the relationships and interactions between different components or modules of a system is a critical aspect of software development. It facilitates maintenance, scalability and code reuse by ensuring that these components work together seamlessly.

Dependency injection (DI) is a key technique for managing dependencies. DI is a design pattern that removes the responsibility for creating and managing dependencies from the classes that use them, thus promoting loose coupling and separation of concerns. Instead, the dependency is added to the class from outside the class.

### What does DM bring?
- **Component decoupling**

DI helps to decouple components by abstracting their dependencies. This reduces the direct dependencies between classes, making them more modular and independent. As a result, changes to one component are less likely to have ripple effects throughout the system.

- **Simple to test**

Dependencies can be easily mocked or stubbed out when unit testing with DI. By injecting test doubles such as fakes or mocks into the code being tested, developers isolate the behaviour of individual components and write more robust and reliable tests.

- **Enhance the reusability of code**

DI allows for greater code reusability. Dependencies can easily be reused in other parts of the system by separating them from the classes that use them. This encourages more modular design and reduces duplicated coding.

- **Agility and maintainability**

DI enables flexible configuration of dependencies. You can easily replace one implementation with another or introduce a new dependency without changing existing code. This flexibility makes the system easier to adapt to changing requirements and makes maintenance easier.

- **Simplified code architecture**

By clearly separating concerns, DI helps to keep the codebase cleaner and more readable. With the explicit declaration of dependencies and their injection into classes, the code structure is more transparent and easier to understand. This makes it easier for developers to reason about the code, identify potential problems and make changes or improvements.

```ruby
# Without DI

class OrderProcessor
  def process(order)
    inventory = Inventory.new
    payment_gateway = PaymentGateway.new

    # ... process the order using inventory and payment_gateway ...
  end
end

# Test for OrderProcessor
describe OrderProcessor do
  describe '#process' do
    it 'processes the order correctly' do
      # Difficult to isolate and mock/stub Inventory and PaymentGateway
    end
  end
end

# With DI

class OrderProcessor
  def initialize(inventory, payment_gateway)
    @inventory = inventory
    @payment_gateway = payment_gateway
  end

  def process(order)
    # ... process the order using @inventory and @payment_gateway ...
  end
end

# Test for OrderProcessor
describe OrderProcessor do
  describe '#process' do
    it 'processes the order correctly' do
      inventory = double('Inventory')
      payment_gateway = double('PaymentGateway')

      # Mock or stub behavior of Inventory and PaymentGateway

      order_processor = OrderProcessor.new(inventory, payment_gateway)
      expect { order_processor.process(order) }.to ...
    end
  end
end
```

## Chain of responsibility
### What is chain of responsibility?
CoR patterns are behavior-oriented design patterns in which requests are passed through a series of potential handlers until they are handled or reach the end of the series.
Any agent in the chain can choose to handle the request or hand it off to the next agent.
This pattern promotes loose coupling and flexibility in the handling of queries, which makes the pattern useful in scenarios with multiple handler choices and dynamic handling needs.
### What does Organiser bring?
- **Decoupling**
  The pattern promotes loose coupling between the sender of the request and the handlers, allowing them to vary independently.
- **Flexibility**
  New handlers can be added or existing ones modified without affecting the sender or other handlers in the chain.
- **Extensibility**
  The pattern allows for easy extension by adding new handlers to the chain.
- **Dynamic behavior**
  The specific handler for a request is determined at runtime, providing flexibility in handling requests based on different conditions.
- **Single Responsibility**
  Each handler in the chain focuses on a specific responsibility, making the code more modular and maintainable.

### What are the constraints?
- **Potential request leakage**
  If a request reaches the end of the chain without being handled, it may not receive appropriate handling or feedback.
- **Performance impact**
  Depending on the length and complexity of the chain, there might be a performance overhead due to iterating through each handler in the chain.
- **Difficulty in debugging**
  As the request traverses through multiple handlers, tracking and debugging the flow can be challenging, especially if there are multiple branches or conditional logic involved.

```ruby
module Orders
  class UpdateOrder
    extend LightService::Organizer

    def self.call(params)
      with(params: params)
        .reduce(
          Steps::ValidateInputParams,
          Steps::FindOrCreateOrder,
          Steps::UpdateOrderAttributes,
          Steps::SendSignalToQueue,
        )
    end
  end
end

module Orders
  module Steps
    class ValidateInputParams
      extend LightService::Action

			expects :params
			promises :schema

      executed do |context|
				context.schema = Orders::Schemas::Params.new.call(context.params)
        context.fail_and_return!("Invalid order params") if context.schema.failure?
      end
    end

    class FindOrCreateOrder
      extend LightService::Action

      executed do |context|
        # find or create the order here
        # ...
        context.order = order
      end
    end

    class UpdateOrderAttributes
      extend LightService::Action

      executed do |context|
        # update order attributes and validate the model
        # ...
        context.fail_and_return!("Invalid order attributes") if invalid
      end
    end

    class SendSignalToQueue
      extend LightService::Action

      executed do |context|
        # send signal to SQS queue
        # ...
      end
    end
  end
end
```
## Referrals

- [Architectural Patterns Catalogue](https://refactoring.guru/design-patterns/catalog)
- [Chain of responsibility pattern](https://refactoring.guru/design-patterns/chain-of-responsibility)
- [Command pattern](https://refactoring.guru/design-patterns/command)
- [Outbox pattern](https://microservices.io/patterns/data/transactional-outbox.html)
- [Async job](https://preparingforcodinginterview.wordpress.com/2019/12/18/design-a-distributed-delayed-job-queueing-system/)

# Framework and libraries

- DRY: A library that helps to reduce code duplication and promotes a DRY (Don't Repeat Yourself) coding style. It provides utility classes and methods that can be used across different parts of the application to avoid writing similar code repeatedly.
- LightService: A library that helps to encapsulate business logic into a single object, making it easier to manage and test. It allows developers to define a set of actions that need to be performed to accomplish a specific task.
- Rails: A full-stack web application framework that provides a set of tools and conventions for building web applications. It includes features like an ORM (Object-Relational Mapping) system, a request/response cycle, routing, and more.
- JSONAPI: A library that provides a standardized way to design and document JSON APIs. It helps to define a clear structure for requests and responses and makes it easier to communicate with clients.
- Grape: A lightweight framework for building RESTful APIs in Ruby. It provides a DSL (Domain-Specific Language) for defining endpoints, and supports various authentication and authorization strategies.
- Swagger: A set of tools for designing, building, documenting, and consuming RESTful APIs. It provides a standardized way to describe API endpoints and their parameters, responses, and authentication requirements.

## Referrals

- [JSONAPI Specification](https://jsonapi.org/)
- [LightService](https://github.com/adomokos/light-service)
- [Ruby On Rails](https://rubyonrails.org/)
- [Grape](https://github.com/ruby-grape/grape)
- [Swagger](https://medium.com/@sushildamdhere/how-to-document-rest-apis-with-swagger-and-ruby-on-rails-ae4e13177f5d)
- [DRY](https://dry-rb.org/)

# Testing

Testing is a vital part of the software development process. It ensures that our code works as intended and catches any bugs or problems before they reach production.
## Best practices
### Write tests early and often
Tests should be written as early as possible in the development process and run frequently to ensure that code changes do not introduce new problems.

### Use automated testing
Automated tests allow you to test quickly and consistently, and are more efficient and reliable than manual tests. This includes unit testing, integration testing and end-to-end testing.
### Test for different scenarios
  Make sure that you test for both the normal and the edge cases, as well as for any error conditions that might occur. This includes testing for invalid input, testing for unexpected behaviour and testing for failure modes.
### Keep tests isolated
  Tests should be written to be independent of each other, that is, the result of one test should not affect the result of another. This ensures that tests are reliable and can be run in any order.

### Use code coverage tools
  Code coverage tools can help identify under-tested areas of code, enabling more comprehensive testing.

## Levels of testing
### Unit Testing
Boundary: Individual units (methods, functions, or classes).
Dependencies: External dependencies are mocked or stubbed.
What should be present: Test cases covering all code paths and edge cases.
What should not be present: External integrations, dependencies on other units or modules.
### Integration Testing
Boundary: Interaction and compatibility between different components/modules.
Dependencies: Integration points between components, including databases, APIs, etc.
What should be present: Test scenarios covering component interaction and data consistency.
What should not be present: In-depth unit-level testing, external factors beyond integration boundaries.
### System Testing
Boundary: The entire system or application as a whole.
Dependencies: Integrated components and external dependencies.
What should be present: End-to-end test cases, user workflows, input/output validation.
What should not be present: Detailed unit-level testing, isolated component testing.
### End-to-End Testing
Boundary: Testing the entire application workflow.
Dependencies: All integrated components, external systems, and user interactions.
What should be present: Test cases covering complete user journeys and system behavior.
What should not be present: Testing individual components in isolation, unit-level testing.
## Referrals

- [How to write good tests](https://leanylabs.com/blog/good-unit-tests/)

# Metrics and measurements

Metrics and analysis are crucial for identifying bottlenecks and improving the performance and scalability of Ruby applications. Here are some important points to consider when designing and analyzing metrics:

## Key principles
### Define clear objectives
Before designing metrics, it is important to clearly define the objectives of the application and the specific areas that need to be measured, both technically and in terms of business goals.
### Measure the right things
To gain meaningful insights, it is important to measure the right things. Metrics should cover key areas of the application, including response times, error rates, and resource usage. It is also important to cover all layers of the application, including the database, application server, and web server.
### Use a consistent naming convention
To make metrics easier to analyze, it is important to use a consistent naming convention. This will help group related metrics together and make it easier to compare metrics across different parts of the application.

### Set baselines and benchmarks
To track performance over time, set baselines and benchmarks for key metrics. This will help identify performance trends and spot deviations from expected performance.

## Examples

**Increment**

```ruby
require 'datadog/statsd'

statsd = Datadog::Statsd.new

def handle_request(endpoint)
  # Do some processing
  statsd.increment("endpoint.requests", tags: ["endpoint:#{endpoint}"])
end
```

**Timings**

```ruby
require 'datadog/statsd'

statsd = Datadog::Statsd.new

def process_data(data)
  start_time = Time.now
  # Do some processing
  end_time = Time.now
  duration = (end_time - start_time) * 1000.0
  statsd.measure("data.processing_time", duration, tags: ["data_type:#{data.class}"])
end
```

**Tracking size of something**

```ruby
require 'datadog/statsd'

statsd = Datadog::Statsd.new

def process_data(data)
  statsd.gauge("data.size", data.size)
  # Do some processing
end
```

# Logging

Logging is an essential part of any application's development and operation. It helps developers to diagnose issues, monitor performance, and gain insights into how the application is behaving in production.

- Choose an appropriate log level
    - Log messages should be categorized by their level of importance. The most commonly used log levels are DEBUG, INFO, WARN, ERROR, and FATAL. It's important to choose the appropriate log level for each message to ensure that important events are not lost in a sea of less important messages.
- Produce meaningful log messages
    - Log messages should be clear and concise, and should provide enough information to help diagnose issues. The message should include relevant context, such as the source of the event, the action being taken, and any relevant data. Avoid using vague or ambiguous language that can make it difficult to understand what happened.
- Include relevant information
    - In addition to the message itself, log entries should include relevant information such as the timestamp, the severity level, the source of the event, and any relevant metadata. It's important to avoid including sensitive information like passwords or other confidential data in log entries.

## Examples

```ruby
require 'semantic_logger'

# Set up the logger
SemanticLogger.add_appender(io: STDOUT, level: :trace)
logger = SemanticLogger['MyApp::MyClass']

# Log a debug message with some metadata
logger.debug('Debug message', some_data: 'some value', another_data: 'another value')

# Log an info message with some additional context
logger.info('Info message', user_id: 12345)

# Log a warning message with some additional context
logger.warn('Warning message', user_id: 12345, error_message: 'Something went wrong')

# Log an error message with an exception
begin
  # Some code that raises an exception
rescue StandardError => e
  logger.error('Error message', exception: e)
end
```

# Error handling

Error handling and error tracking are critical aspects of software development. Errors can occur at any time during the execution of an application. Without proper handling and tracking mechanisms, it can be difficult to identify the root cause of issues and take corrective action.

Proper error handling ensures that errors are caught and dealt with gracefully and informatively. This can help prevent the application from crashing and provide users with helpful error messages that guide them towards a resolution.

Furthermore, error tracking provides valuable insights into the application's performance. This helps developers identify recurring issues, optimize. the code, and improve the overall user experience.

Investing time and effort in proper error handling and error tracking can save time and resources in the long run. By reducing the occurrence of errors and quickly resolving issues when they do occur, developers can improve the reliability of their applications and provide a better user experience.

## Examples

```ruby
require 'sentry-ruby'
require 'dry-container'

class ApplicationContainer
  extend Dry::Container::Mixin

  register :sentry do
    Sentry::Client.new
  end
end

class SampleService
  include LightService::Action
	include Import[:sentry]

  def execute
    # business logic goes here
    rescue StandardError => e
      sentry.capture_exception(e)
      failure(:something_went_wrong)
    end
  end
end
```