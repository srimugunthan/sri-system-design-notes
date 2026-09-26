SOLID is a set of five object-oriented design principles meant to make code easier to maintain, extend, and test.
<img width="660" height="854" alt="image" src="https://github.com/user-attachments/assets/88c241f5-9140-42e6-a506-4ba8bdd43091" />


**S — Single Responsibility Principle**
A class should have only one reason to change. Each class should do one job. If a `UserManager` class handles authentication, database access, and email notifications, it has three responsibilities — split it into separate classes so a change in one concern doesn't ripple into unrelated code.

**O — Open-Closed Principle**
Classes should be open for extension but closed for modification. Instead of editing existing code every time a new case shows up, design so new behavior can be added by extending (e.g., new subclasses or implementations) rather than changing tested code. Typically achieved with abstraction — interfaces or base classes that new implementations plug into.

**L — Liskov Substitution Principle**
Subtypes must be substitutable for their base types without breaking the program. If `Bird` has a `fly()` method and `Penguin extends Bird`, but penguins can't fly, that's a violation — code expecting a `Bird` shouldn't break when handed a `Penguin`. It's about behavioral correctness of inheritance, not just matching method signatures.

**I — Interface Segregation Principle**
Clients shouldn't be forced to depend on methods they don't use. Prefer several small, specific interfaces over one large general-purpose interface. A `Worker` interface with `work()` and `eat()` forces a `RobotWorker` to implement `eat()` meaninglessly — split into `Workable` and `Eatable` instead.

**D — Dependency Inversion Principle**
High-level modules shouldn't depend on low-level modules; both should depend on abstractions. Instead of a `PaymentService` directly instantiating a `StripeGateway`, it should depend on a `PaymentGateway` interface, with the concrete implementation injected. This decouples modules and makes swapping implementations (or mocking for tests) straightforward.

Together, these principles push toward code that's loosely coupled, where dependencies point at abstractions rather than concrete details, and where change in one part of a system doesn't force cascading edits elsewhere — particularly relevant when building modular ML/agentic pipelines where components (data loaders, model backends, guardrail checks) need to be swapped without rewriting the whole system.
