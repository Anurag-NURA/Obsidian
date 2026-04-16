Design patterns are essentially reusable solutions to common problems in software design. They offer a standardized way to tackle recurring challenges in object-oriented software development. Each pattern provides a template that can be used in various contexts to solve similar problems.

`Think of them as blueprints for building software that is more efficient, maintainable, and scalable. They help developers create software that is easier to understand, change, and extend over time.`
# Three main categories of Patterns:

![[Pasted image 20250108102015.png]]

1. **Creational Patterns:** `Instead of creating objects directly, these patterns give you more flexibility in how objects come into existence.`
2. **Structural Patterns**: These patterns deal with object composition, ensuring that if one part of a system changes, the entire system doesn't need to change with it. Examples include the Adapter, Composite, and Decorator patterns. `Deals with how objects relate to each other. Think of them as blueprints for building larger structures from individual pieces.` 
3. **Behavioral Patterns**: These patterns are concerned with communication between objects. They help make the interactions between objects more flexible and easier to implement. Examples include the Observer, Strategy, and Command patterns. `Handle communication between objects - how they interact and distribute responsibility.`

## Creational Patterns

 These patterns deal with object creation mechanisms, trying to create objects in a manner suitable to the situation. Examples include the Singleton, Factory, and Builder patterns. 

Most commonly used creational design patterns:

1. **Singleton Pattern**
	 **Purpose**: Ensures that a class has only one instance and provides a global point of access to it. 
	 **Use Case**: Useful for logging, drivers, caching, and thread pools. 

![[Pasted image 20250108103732.png]]
In the provided Image, instead of creating multiple loggers writing to the same Log file. It is better to have one central Logger instance to handle everything.

![[Pasted image 20250108104214.png]]
If multiple Logger instances are created to handle a Log file then it can create multiple conflicts between File Lock whenever a logger writes in the Log file.

Code Example:
![[Pasted image 20250108104446.png]]

Good example only have a single instance that can be access globally. This can be also used when we are connecting to the Database connection pool or Logger as seen above. 

![[Pasted image 20250108104739.png]]

![[Pasted image 20250108104749.png]]

- **Testing can be a nightmare**: Singletons can be problematic in unit testing because they maintain state between tests. This can lead to tests influencing each other, making debugging and isolation of tests harder. Mocking Singletons for testing purposes also becomes challenging.
- **Concurrency Issues**: Also in multithreaded environment we need a better handling for prevent creating multiple instances. In multi-threaded applications, ensuring that only one instance of the Singleton is created can be tricky. Without proper synchronization, multiple threads might create multiple instances of the Singleton simultaneously, defeating its purpose.
- **Violation of Single Responsibility Principle:** Singletons can sometimes end up doing more than they should, violating the Single Responsibility Principle. Since they are globally accessible, they may accumulate responsibilities that don't belong to them.