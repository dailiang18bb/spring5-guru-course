
# Spring Framework 5: Beginner to Guru
Start Date: 06/29/2020


### Utilize the learning content
- Follow along with the code examples
- Leverage the GitHub for branches, compares, and forks
- Join the Slack, ask questions


### Get help when stuck
- Q&A inside the courses
- [FAQ](https://github.com/springframeworkguru/spring5webapp/wiki)
- Slack
- Stack overflow
- gitter



## Course Content
---
### Building a Spring Boot Web App
#### Spring initializr
save a lot works on congiure and wire the dependency of spring applications


#### JPA
- leakage
map java class into JPA entities
- JPA and Hibernate generate all the SQL for us, same us times


#### Equality
- The Id property is mapped to the primary key in the underlying database. Thus it is used to persist and retrieve object from the database.
- Override `equals()`, `hashcode()` method. We need to change it to base equality on ID of the object.
- Override `toString()` method, to make it show object properties information. The Default method can only get the class or Object ID.

#### Data Repository
- Repository object is responsible for persistence and query operation

#### h2 database
- need to manual config database url since springboot 2.3.x
```
[/application.properties]
spring.h2.console.enabled=true
spring.datasource.driver-class-name=org.h2.Driver
spring.datasource.url=jdbc:h2:mem:mydb
spring.datasource.data-username=sa
```

#### MVC and Spring MVC
- MVC => Model, View, Controller, common web design pattern.
- Spring MVC =>
```
                        handler mapping
                          ||
Client request => dispatcher servlet => controller => service => data
                        ||    |------Model----|
                       View(JSP, Thymeleaf)
```

#### Controller config
- No, Spring will not 'see' the controller class. The @Controller annotation tells the Spring Framework this class is to be added into the Spring Context as a controller.

#### Thymeleaf
- is a Java template engine, alternitive to JSP

---
### Spring Pet Clinic project
- [Pet Clinic canonical spring boot version](https://github.com/spring-projects/spring-petclinic)
- [Pet Clinic other version](https://github.com/spring-petclinic)

#### Workflow
1. Initialize the Spring project from Scratch.
2. Setup git and ignore, and create issues as TODO plan

#### S.O.L.I.D principles of OOP, by Uncle Bob
##### Lead to better quality code, more testable and easier to maintain.
- [S] `Single responsibility principle`, just because you can doesn't mean you should.
> goal: ensuring small, focused, and highly cohesive software components, concerned with classes

 - Every class should have a single responsibility.
 - There should never be more than one reason for a class to change.
 - Your classes should be small, no more than a screen full of code.
 - Avoid "god" classes.
 - Split big classes into small classes.


- [O] `Open closed principle`, open chest surgery is not needed when putting on a coat.
> [insurance system] example, use abstract class for open.

  - Your classes should be open for extension.
  - But closed for modification.
  - You should be able to extend a classes behavior, without modifying it.
  - Use private variables with getters and setters, only when you need them.
  - Use abstract base classes.


- [L] `Liskov Substitution principle`, If it looks like a duck, quacks like a duck, but needs batteries - You probably have the wrong abstraction.
 - Objects in a program would be replaceable with instances of their subtypes WITHOUT altering the correctness of the program.
 - Violations will often fail the "is a" test.
 - A Square "is a" Rectangle.
 - However, a Rectangle "is NOT" a Square.


- [I] `Interface Segregation principle`, you want me to plug this in, where?
> while writing interface keep in mind of this principle  
> goal: ensuring small, focused, and highly cohesive software components, concerned with Interfaces.

 - Make fine grained interfaces that are client specific.
 - Many client specific interfaces are better than one "general purpose" interface.
 - Keep your components focused and minimize dependencies between them.
 - Notice relationship to the Single Responsibilities Principle.
 - Avoid "fat interfaces", use "role interfaces", which declares one or more methods for a specific behavior.


- [D] `Dependency Inversion Principle`, would you solder a lamp directly to the electrical wiring in a wall?
> keeping your code loosely coupled, high-level class avoid depend on low-level class, depend on interface instead.    
>[Light bulb]example

 - Abstractions should not depend upon details.
 - Detail should depend upon abstractions.
 - Important that higher level and lower level objects depend on the same abstract interaction.
 - This is NOT the same as Dependency Injection - which is how objects obtain dependent objects.


### Spring Context
- when the controller ask for a component, it ask the application context to see if there is one or construct one,
- Have the application context to create and manage the instance of Objects.

### Dependency injection


- "When you feel like eating Pizza, you either create it or order it from a Pizza store"
- The second option is much easier right? Same for programmers.
- Without DI, in large applications, we programmers have to programmatically create all the objects, manage the mapping between them, and programmatically handle any lifecycle events. So programmers have control of everything. It's OK for a  small Hello World applications, but when you thing enterprise-grade applications with hundreds and thousands of objects, this becomes tedious and error-prone.
- So Spring applied IoC, which is Inversion of Control. Now instead of the programmer, control is inversed, the Spring Framework has the control. We simply order Spring where we need any dependencies, and Spring will create, manage, and inject it at the point we asked for.


#### Type of Dependency Injection
- By class properties - least preferred
- By setters - much debate
- By `Constructor` - Most preferred

#### Concrete classes vs interfaces
- Generally DI with concrete classes should be avoided.
- DI via interface is highly preferred.

#### Inversion of control - aka IoC
- The runtime environment which injects dependencies.
- The Spring framework is going to control most of the activity and structure, programmer going to code to fulfill the business.

#### Best practice with DI
- Favor using Constructor Injection over Setter Injection.
- Use final properties for injected components.
- Whenever practical, code to an interface.

#### @Qualifier Annotation
- By default, Spring resolves autowired entries by type.
- If more than one bean of the same type is available in the container, the framework will throw NoUniqueBeanDefinitionException, indicating that more than one bean is available for autowiring.
- By using the @Qualifier annotation, we can eliminate the issue of which bean needs to be injected.
- By including the @Qualifier annotation together with the name of the specific implementation we want to use.

#### @Primary Annotation
- When there is no @Qualifier, and context confused on which bean should be injected, it can go for the @Primary one.


#### Spring Profile
- Profiles are a core feature of the framework – allowing us to map our beans to different profiles – for example, dev, test, prod.

#### Bean lifecycle


### Spring Configuration
#### XML based Configuration
 - Introduced in Spring Framework 2.0, still supported in Spring Framework 5.x

#### Annotation based Configuration
 - Introduced in Spring Framework 3.0.
 - Spring beans pick up by Component Scan, refers to class level annotations `@Controller`, `@Service`, `@Component`, `@Repository`

#### Java based Configuration, [Preferred]
  - Introduced in Spring Framework 3.0.
  - Use Java classes to define Spring beans, declared with `@Bean` annotation.
  - Configuration class declared with `@Configuration` annotation.

#### Groovy Bean Definition DSL Configuration
  - Introduced in Spring Framework 4.0.
  - Allows you to declare beans in Groovy(Grails)


### Spring Framework Stereotypes
 - `@Component`, indicate the class is a component, will be created as a bean.
 - `@Controller`, indicate the class has a role of Spring MVC Controller, handle http request and response.
 - `@RestController`, extends @Controller, add @ResponseBody
 - `@Repository`, a mechanism for encapsulating storage, retrieval and search behavior
 - `@Service`, managing the controller with data, repository inject into service, service inject into controller.

### Spring Component Scan
 - Will Scan Spring Stereotypes annotations.
 - Component scan will always get used. If you follow the conventions, you don't need to explicitly specify it. If you don't follow, you specify the folders or classes to scan using @ComponetScan

### Spring Factory Bean


### Spring Boot Configuration
 - Maven and Gradle are supported for curated dependencies.
 - Maven project inherit from a Spring Boot Parent POM, don't specify dependency version, let it inherit from parent.
 - `Spring Boot Starters` are top level dependencies for popular java libraries, will bring in related Spring component and dependencies.
 - `@SpringBootApplication` annotation inclues `@Configuration`, `@EnableAutoConfiguration`, `@ComponentScan`.


### Spring Bean Scopes
 - Singleton - (default) Only one instance of the bean is created in the IoC container.
 - Prototype - A new instance is created each time the bean is requested.
 - Request - A single instance per http request. Only valid in the context of a web-aware Spring ApplicationContext.
 - Session - A single instance per http session. Only valid in the context of a web-aware Spring ApplicationContext.
 - Global-session - A single instance per global session. Typically Only used in a Portlet context. Only valid in the context of a web-aware Spring ApplicationContext.
 - Application - bean is scoped to the lifecycle of a ServletContext. Only valid in the context of a web aware.
 - Websocket - Scopes a single bean definition to the lifecycle of a WebSocket. Only valid in the context of a web-aware Spring ApplicationContext.
 - Use `@Scope` annotation or XML attribute of bean tag.


### Q&A
1. Why do we need BaseEntity?
 - You don't have to add id property for every class just extend it and you have a id property for your class. Reduces writing boiler plate code.
 - Also, what if you want to change the ID generation strategy? Instead of modifying each entity, you now can update only BaseEntity.
