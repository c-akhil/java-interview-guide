# 🚀 Java & Spring Boot Interview Preparation

This document covers essential interview questions for Java and Spring Boot in the exact order provided.

---

## 📌 Core Java Concepts

### 1. What are the main features of Java?
Java is a high-level, object-oriented programming language known for:
- **Platform Independence**: Java programs run on any platform with a JVM ("Write Once, Run Anywhere").
- **Object-Oriented**: Supports principles like encapsulation, abstraction, inheritance, and polymorphism.
- **Automatic Memory Management**: Uses a garbage collector to manage memory.
- **Multithreading**: Enables concurrent execution of two or more parts of a program.
- **Robustness**: Provides strong type checking, exception handling, and eliminates issues like explicit pointer manipulation.
- **Security**: Includes features like bytecode verification, a security manager, and class loaders.
- **Performance**: Utilizes a Just-In-Time (JIT) compiler for efficient execution.

---

### 2. What is the difference between JDK, JRE, and JVM?
| Feature | JDK (Java Development Kit) | JRE (Java Runtime Environment) | JVM (Java Virtual Machine) |
|---------|----------------------------|-------------------------------|----------------------------|
| **Definition** | A complete toolkit for Java development (includes the compiler and other tools). | Provides the environment required to run Java applications. | An engine that executes Java bytecode. |
| **Components** | Contains the JRE, compiler (`javac`), and debugging tools. | Includes the JVM and core libraries. | Converts `.class` files into machine-specific code. |
| **Usage** | Used for both developing and running Java applications. | Needed only for running Java applications. | Works behind the scenes to run Java programs. |

---

### 3. How does memory management work in Java?
Java manages memory automatically with:
- **Heap Memory**: Where all the class instances and objects are stored.
- **Stack Memory**: Stores method frames, including local variables and method calls.
- **Metaspace (formerly PermGen)**: Stores class metadata.
- **Garbage Collector (GC)**: Periodically reclaims memory from objects that are no longer in use.

---

### 4. What is the difference between `==` and `.equals()`?
| Operator    | Purpose                                           | Example                                    |
|-------------|---------------------------------------------------|--------------------------------------------|
| `==`        | Checks if two object references point to the same memory location. | `s1 == s2` returns `false` for two distinct objects with the same content. |
| `.equals()` | Compares the actual content of the objects (if overridden properly). | `s1.equals(s2)` returns `true` if the contents are identical. |

*Example:*
```java
String s1 = new String("Hello");
String s2 = new String("Hello");
System.out.println(s1 == s2);      // false
System.out.println(s1.equals(s2)); // true
```
### 5. What is the purpose of final, finally, and finalize()?
Keyword	Purpose
final	Used to declare constants, prevent method overriding, and stop inheritance.
finally	A block that always executes after try-catch blocks, used for cleanup code.
finalize()	A method called by the garbage collector before an object is destroyed (deprecated in newer Java versions).
## 📌 OOP in Java
### 6. What are the four main principles of OOP?
Encapsulation: Bundling data and methods that operate on the data within a single unit (class).
Abstraction: Hiding complex implementation details and exposing only the necessary parts.
Inheritance: Creating new classes from existing ones, promoting code reuse.
Polymorphism: Allowing methods to perform different tasks based on the object that invokes them.
### 7. What is method overloading vs method overriding?
Aspect	Method Overloading	Method Overriding
Definition	Multiple methods in the same class with the same name but different parameters.	A subclass provides a specific implementation for a method already defined in its superclass.
Scope	Within the same class.	Across a superclass and its subclass.
Return Type	Can vary (subject to rules).	Must be the same (or covariant) as in the superclass.
### 8. What is abstraction, and how is it implemented?
Abstraction involves hiding the complex implementation details and exposing only the necessary functionality. It can be implemented using:

Abstract Classes: Classes declared with the abstract keyword that can include both abstract and concrete methods.
Interfaces: Define methods that must be implemented by a class; Java 8+ allows default and static methods.
### 9. What are access modifiers in Java?
Access modifiers determine the visibility of classes, methods, and variables:

private: Accessible only within the same class.
default (no modifier): Accessible within the same package.
protected: Accessible within the same package and subclasses.
public: Accessible from any other class.

| Modifier  | Class | Package | Subclass | World |
|-----------|-------|---------|----------|-------|
| `private` | ✅ | ❌ | ❌ | ❌ |
| `default` | ✅ | ✅ | ❌ | ❌ |
| `protected` | ✅ | ✅ | ✅ | ❌ |
| `public` | ✅ | ✅ | ✅ | ✅ |

### 10. What is the difference between an interface and an abstract class?
Feature	Abstract Class	Interface
Methods	Can have both abstract and concrete methods.	All methods are abstract by default (Java 8+ allows default and static methods).
Fields	Can have instance variables.	Only constants (implicitly public static final).
Inheritance	Supports single inheritance.	Supports multiple inheritance (a class can implement multiple interfaces).
## 📌 Collections & Data Structures
### 11. What are key interfaces in Java Collections?
Key interfaces include:

List: An ordered collection (e.g., ArrayList, LinkedList).
Set: A collection that does not allow duplicate elements (e.g., HashSet, TreeSet).
Queue: Typically used to hold elements prior to processing (e.g., LinkedList, PriorityQueue).
Map: An object that maps keys to values (e.g., HashMap, TreeMap).
### 12. How does HashMap work internally?
Buckets: Uses an array of buckets where each bucket is essentially a linked list (or a balanced tree if many collisions occur).
Hashing: The key's hashCode() is used to compute an index for the bucket.
Collision Handling: When multiple keys hash to the same bucket, they are stored in a list or tree structure within that bucket.
### 13. What is the difference between ArrayList and LinkedList?
Aspect	ArrayList	LinkedList
Underlying Structure	Dynamic array.	Doubly linked list.
Access Time	Fast random access (O(1)).	Slower random access (O(n)).
Insertion/Deletion	Slower for middle operations (requires shifting elements).	Faster insertions and deletions (especially at the beginning or end).
### 14. How do you remove duplicate elements from a list?
You can remove duplicates by converting the list into a set (which doesn’t allow duplicates) and then back to a list. For example:

java
```
List<Integer> list = Arrays.asList(1, 2, 2, 3, 4, 4);
Set<Integer> set = new HashSet<>(list);
List<Integer> uniqueList = new ArrayList<>(set);
```
Or using Java 8 Streams:

java
```
List<Integer> uniqueList = list.stream()
                               .distinct()
                               .collect(Collectors.toList());
```
### 15. What is a ConcurrentHashMap, and why is it useful?
ConcurrentHashMap is a thread-safe version of HashMap that:

Allows concurrent read and write operations.
Uses a segmented locking mechanism (or finer-grained locks in Java 8+) to reduce contention.
Is useful in multi-threaded applications where high concurrency is needed.
## 📌 Java 8 & Functional Programming
### 16. What are lambda expressions in Java?
Lambda expressions are a way to write anonymous functions (i.e., functions without a name) that can be treated as objects. They provide a clear and concise way to represent one method interface using an expression.

java
```
Runnable r = () -> System.out.println("Hello, Lambda!");
```
### 17. What is the Streams API, and why is it useful?
The Streams API enables functional-style operations on streams of elements (such as collections). It allows for operations like filtering, mapping, and reducing without modifying the underlying data source. It also supports parallel processing.

java
```
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
List<Integer> squares = numbers.stream()
                               .map(n -> n * n)
                               .collect(Collectors.toList());
```
### 18. What is the difference between map(), flatMap(), and filter()?
map(): Applies a given function to each element of the stream and returns a stream of the results.
flatMap(): Similar to map(), but each element is replaced with a stream of new values, and then all the streams are flattened into a single stream.
filter(): Evaluates each element against a predicate and returns a stream that includes only those elements that match the predicate.
### 19. What are Optional classes, and how are they useful?
The Optional class is a container that may or may not contain a non-null value. It helps in avoiding NullPointerException and provides methods to safely handle the presence or absence of a value.

java
```
Optional<String> optionalName = Optional.ofNullable(getName());
optionalName.ifPresent(name -> System.out.println("Name: " + name));
```
### 20. What are default and static methods in interfaces?
Default Methods: Allow an interface to provide a default implementation so that classes implementing the interface are not forced to implement them.
Static Methods: Belong to the interface itself rather than any instance, and can be invoked without an implementation class.
java
```
public interface MyInterface {
    default void defaultMethod() {
        System.out.println("Default method");
    }
    static void staticMethod() {
        System.out.println("Static method");
    }
}
```
## 📌 Spring Boot & Microservices
### 21. What is Spring Boot, and why is it popular?
Spring Boot is a framework that simplifies the development of Spring-based applications by:

Providing auto-configuration to reduce manual setup.
Offering embedded servers (e.g., Tomcat, Jetty) for standalone applications.
Reducing boilerplate code and easing dependency management.
Being production-ready with built-in metrics, health checks, and externalized configuration.

### 22. What are key annotations in Spring Boot?

Some of the key annotations include:

@SpringBootApplication: Enables auto-configuration and component scanning.

@RestController: Marks a class as a controller where every method returns a domain object rather than a view.

@Service, @Repository, @Component: Stereotype annotations to indicate the role of a class.

@Autowired: Enables automatic dependency injection.

### 23. How does Spring Boot handle database connections?
Spring Boot simplifies database connectivity by:

Using Spring Data JPA or JDBC templates.
Auto-configuring data sources and connection pools (HikariCP is the default).
Allowing configuration via application.properties or application.yml files:
properties
```
spring.datasource.url=jdbc:mysql://localhost:3306/mydb
spring.datasource.username=root
spring.datasource.password=root
```
### 24. What is dependency injection?
Dependency Injection (DI) is a design pattern where an object’s dependencies are provided by an external entity (like the Spring container) rather than being created by the object itself. This promotes loose coupling and easier testing.

### 25. What is the purpose of @Transactional?
The @Transactional annotation is used to define the scope of a single database transaction. It ensures that all operations within the annotated method are executed within a transaction boundary. If any operation fails, the transaction is rolled back, ensuring data integrity (ACID properties).

## 📌 Spring Boot & API Development
### 26. What is REST, and how does Spring Boot implement it?
REST (Representational State Transfer) is an architectural style for designing networked applications. Spring Boot implements RESTful web services using:

@RestController for creating controllers.
Mapping annotations such as @RequestMapping, @GetMapping, and @PostMapping.
JSON (or XML) as the data interchange format.
### 27. What is the difference between @GetMapping and @PostMapping?
Annotation	HTTP Method	Purpose
@GetMapping	GET	Retrieves data from the server.
@PostMapping	POST	Submits data to the server.
### 28. How does Spring Boot handle authentication? (JWT, OAuth)
Spring Boot, along with Spring Security, supports various authentication methods:

JWT (JSON Web Token): A stateless, token-based authentication method.
OAuth 2.0: An industry-standard protocol for authorization that can also handle authentication. These methods secure REST endpoints and manage user sessions or stateless interactions.
### 29. What are the best practices for designing REST APIs?
Some best practices include:

Use the correct HTTP methods (GET, POST, PUT, DELETE).
Use meaningful and resource-based URIs.
Implement proper error handling and status codes.
Support pagination, filtering, and sorting.
Document the API (e.g., using Swagger/OpenAPI).
Secure endpoints using authentication and authorization.
### 30. How does Spring Boot handle pagination?
Spring Boot integrates with Spring Data, which provides pagination support through the Pageable interface. Repository methods can return a Page<T>:

java
```
Page<User> users = userRepository.findAll(PageRequest.of(0, 10));
```
## 📌 Spring Boot & Microservices Architecture
### 31. What are microservices, and how does Spring Boot support them?
Microservices are an architectural style where an application is composed of small, independent services. Spring Boot supports microservices by simplifying service creation, configuration, and deployment. It works well with Spring Cloud to handle service discovery, configuration, and inter-service communication.

### 32. What is the difference between monolithic and microservices architecture?
Monolithic Architecture: The entire application is built as a single, unified unit.
Microservices Architecture: The application is divided into independent, loosely coupled services that can be developed, deployed, and scaled independently.
### 33. What is API Gateway, and how does it work?
An API Gateway is a single entry point for all client requests to a set of microservices. It handles routing, load balancing, authentication, rate limiting, and other cross-cutting concerns. Examples include Netflix Zuul and Spring Cloud Gateway.

### 34. What is Eureka Server, and how does service discovery work?
Eureka Server is a service registry from Netflix OSS. It allows microservices to register themselves so that they can be discovered by other services. Clients query Eureka to locate instances of a service dynamically.

### 35. What is Circuit Breaker, and how does it improve resilience?
The Circuit Breaker pattern prevents cascading failures by stopping the flow of requests to a failing service after a threshold is reached. It temporarily “opens” the circuit, allowing fallback methods to be invoked until the service recovers. Libraries like Hystrix or Resilience4j provide this functionality.

## 📌 Spring Boot Security & Optimization
### 36. How does Spring Boot implement security best practices?
Spring Boot integrates with Spring Security to implement security best practices such as:

Secure authentication and authorization.
Protection against common vulnerabilities (e.g., CSRF, XSS).
Secure password storage and encryption.
Integration with OAuth2 and JWT for token-based security.
### 37. How can you improve Spring Boot performance?
Performance improvements can include:

Implementing caching mechanisms (e.g., Redis, EhCache).
Optimizing database queries and using efficient connection pooling.
Enabling asynchronous processing where appropriate.
Configuring GZIP compression for responses.
Tuning embedded server settings (e.g., thread pools).
### 38. What is rate limiting, and why is it useful?
Rate limiting restricts the number of requests a client can make within a specified time period. This helps prevent abuse, ensures fair usage, and protects against Denial-of-Service (DoS) attacks.

### 39. What is CORS, and how does Spring Boot handle it?
CORS (Cross-Origin Resource Sharing) is a security feature that restricts how resources on a web server can be requested from another domain. Spring Boot can handle CORS using:

The @CrossOrigin annotation on controllers.
Global configuration through a WebMvcConfigurer bean.
### 40. How does Spring Boot integrate with Kubernetes & Docker?
Spring Boot applications can be containerized using Docker. Once containerized, these applications can be orchestrated using Kubernetes for scaling, load balancing, and managing deployments. Spring Boot’s production-ready features (such as health checks and externalized configuration) make it well-suited for cloud-native environments.
