Design patterns are typically grouped into three categories (the classic Gang of Four taxonomy): **Creational**, **Structural**, and **Behavioral**.

## Creational Patterns
Deal with object creation — decoupling *how* an object is created from *how it's used*.

- **Singleton** — ensures a class has only one instance and provides a global access point to it. Common for config managers, connection pools, loggers.
- **Factory Method** — defines an interface for creating an object but lets subclasses decide which class to instantiate.
- **Abstract Factory** — produces families of related objects without specifying their concrete classes (e.g., a `UIFactory` that creates matching `Button`, `Checkbox`, `Scrollbar` for a given OS theme).
- **Builder** — separates construction of a complex object from its representation, so the same construction process can build different representations (e.g., building a complex `Pizza` object step by step with optional toppings).
- **Prototype** — creates new objects by cloning an existing instance rather than instantiating from scratch.

## Structural Patterns
Deal with how classes/objects are composed to form larger structures.

- **Adapter** — converts the interface of a class into another interface clients expect, letting incompatible interfaces work together (e.g., wrapping a legacy API to match a new one).
- **Decorator** — attaches additional responsibilities to an object dynamically, as a flexible alternative to subclassing (e.g., wrapping a `Coffee` object with `MilkDecorator`, `SugarDecorator`).
- **Facade** — provides a simplified, unified interface to a complex subsystem.
- **Composite** — composes objects into tree structures to represent part-whole hierarchies, letting clients treat individual objects and compositions uniformly (e.g., files and folders).
- **Proxy** — provides a surrogate/placeholder for another object to control access to it (lazy loading, access control, caching, logging).
- **Bridge** — decouples an abstraction from its implementation so the two can vary independently (e.g., separating `Shape` from `Renderer` so shapes and rendering engines evolve independently).
- **Flyweight** — minimizes memory use by sharing common state across many similar objects.

## Behavioral Patterns
Deal with communication and responsibility distribution between objects.

- **Strategy** — defines a family of interchangeable algorithms, encapsulated and selectable at runtime (e.g., swapping sorting algorithms, or different fraud-scoring strategies).
- **Observer** — defines a one-to-many dependency so that when one object changes state, all its dependents are notified automatically (pub/sub, event listeners).
- **Command** — encapsulates a request as an object, allowing parameterization, queuing, undo/redo.
- **State** — allows an object to alter its behavior when its internal state changes, appearing to change its class.
- **Template Method** — defines the skeleton of an algorithm in a base class, letting subclasses override specific steps without changing the algorithm's structure.
- **Chain of Responsibility** — passes a request along a chain of handlers until one handles it (e.g., middleware pipelines, validation chains).
- **Iterator** — provides a way to sequentially access elements of a collection without exposing its underlying representation.
- **Mediator** — centralizes complex communications between related objects so they don't reference each other directly.
- **Visitor** — separates an algorithm from the object structure it operates on, letting you add new operations without modifying the objects.
- **Memento** — captures and restores an object's internal state without violating encapsulation (undo functionality).

## How this connects to SOLID
Many of these patterns are essentially standard, battle-tested ways of *applying* SOLID principles:
- **Strategy** and **Factory patterns** are direct applications of the **Open-Closed** and **Dependency Inversion** principles — new behavior is added via new implementations of an abstraction, not by modifying existing code.
- **Decorator** and **Adapter** follow **Dependency Inversion** — they wrap concrete implementations behind a shared interface.
- **Facade** often helps with **Interface Segregation** from the client's perspective — exposing only what's needed and hiding subsystem complexity.

If you want, I can map specific patterns to a system design you're working on (e.g., something in your guardrails middleware or agent pipelines) — often things like Strategy for pluggable detection rules or Chain of Responsibility for pipeline stages map naturally onto ML/agentic system architectures.
