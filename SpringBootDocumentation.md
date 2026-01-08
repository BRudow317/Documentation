# SpringBoot

## Key Spring Components

### Application Context Container
The core of the Spring Framework that manages the lifecycle and configuration of application components (beans). It's kind of the brain or object factory for the Spring framework. It is responsible for:
- Instantiating beans & creating objects
- Injecting & Configuring dependencies
- Loading configuration metadata (annotations, XML, Java config)
- Managing bean scopes and lifecycles
- Applies cross-cutting logic (AOP, proxies)
- Event publishing and handling

### Inversion of Control (IoC)
A design principle where the control of object creation and management is transferred from the application to a framework or container.

### IoC Container
A framework component that manages the lifecycle and dependencies of application objects (beans) based on configuration metadata. They're really good at managing complex object graphs and dependencies. Which means you don't need to instantiate and wire up everything manually. You can just declare what you need, and the container takes care of the rest.
An IoC container is a framework component that:
- Creates application objects (beans)
- Injects dependencies into them
- Controls their lifecycle
- Manages configuration

IoC Vs Manual DI:
Without IoC:
- You manually `new` every dependency.
- Hard to test; dependencies are hard-coded.
- Tight coupling between classes.
- Hard to manage object lifecycles, they live as long as your code says.

With IoC Container:
- Container constructs and wires everything.
- Easy to mock/inject test doubles.
- Classes depend on interfaces; low coupling.
- Container manages lifecycles (singleton, prototype, request, session).
- Configuration is externalized (annotations, XML, Java config).
- Container handles scope, proxies, AOP.

### Object Dependency
An object that another object relies on to function properly. Objects should not create their own dependencies but have them provided externally (via DI).
```java
public class OrderService {
    // PaymentProcessor is a dependency of OrderService, injected via constructor
    private final PaymentProcessor paymentProcessor;
    public OrderService(PaymentProcessor p) {
        this.paymentProcessor = p;
    }
}
```
### Dependency Injection (DI)
A design pattern where an object's dependencies are provided (injected) by an external entity rather than the object itself.

### Plain Old Java Object (POJO)
A simple Java object that does not adhere to any special framework conventions or requirements.

### lambda operator
The `->` operator in Java used to define lambda expressions, which are a way to represent functional interfaces (interfaces with a single abstract method) in a more concise way.
```java 
// Take the thing on the left and do the thing on the right.
List<String> list = Arrays.asList("a", "b", "c");
list.forEach(item -> System.out.println(item));
```

### DTO (Data Transfer Object)
A simple object used to transfer data between different layers or components of an application, typically without any business logic. They shape network payloads independent of internal models. They also improve security by exposing only necessary fields.
They also provide a layer of abstraction between internal models and external dependencies of that data.

In Spring DTOs are often **@RequestBody** and **@ResponseBody** objects in REST controllers.

## Domain-Driven Design
Domain-Driven Design is a software design approach focused on modeling real world concepts and things to objects, called domain entities. This lets developers and domain experts use the same vocabulary.
Classes represent real-world entities, actions, rules, processes, policies, workflows, and events.
- Domain Layer - Entities, Value Objects, Aggregates (pure business logic)
- Application Layer - Orchestrates use cases (services)
- Infrastructure Layer - Databases, external APIs, messaging, ORM
- UI Layer - Controllers, views, REST, etc.

### Domain Entity
Domain Entities are objects that represent core business concepts and contain business logic. They often map directly to database tables in `ORM frameworks` like **Hibernate**. They're in direct contrast to DTOs. **Child entities** are part of the domain entity but do not have their own identity.

They can perform actions and enforce rules related to the business object/domain entity. 
A domain entity typically has:
- Identity (unique ID)
- Attributes (fields)
- Business methods (logic)
- Relationships (to other entities)
- Remains in state during runtime, and persists in a DB.
```java
@Entity // JPA annotation for DB mapping
public class Order {
    // The domain entity is "Order"
    // It has fields that represent its state.
    private Long id;
    private OrderStatus status;
    private ItemCatalog items;
    // Business Logic Methods that change state.
    public void cancel() {
        if (status == OrderStatus.SHIPPED) {
            throw new IllegalStateException("Cannot cancel shipped order.");
        }
        status = OrderStatus.CANCELLED;
    }
    @Bean
    public void save(){
        // Uses a DTO to transfer data to the DB layer
        DbController dto.OrderDTO(this.id, this.status, this.items);
    }
    @Bean
    public ItemCatalog listItems(Long id){
        ItemCatalog itemsOnOrder.getItemsById(id);
        return itemsOnOrder;
    }
}
```
### JPA Entity
A special type of domain entity that is mapped to a database table using **JPA (Java Persistence API)** annotations. These entities are managed by an **ORM (Object-Relational Mapping) framework like Hibernate**, which handles database interactions automatically.
- JPA treats it as a table mapping.
- Each instance represents a row in that table.
- Fields map to columns (unless ignored).
- JPA/Hibernate can save, update, delete, query, and load it automatically.
```java
import jakarta.persistence.GeneratedValue;
import jakarta.persistence.Entity;
import jakarta.persistence.Id;
@Entity // JPA annotation to mark this as a DB entity
public class Customer {
    @Id // indicates this is a primary key
    @GeneratedValue // Auto-generate ID on object instantiation
    private Long id;
    private String name;
    private int credit;
}
```
Spring Boot typically uses JPA entities as domain entities, but that's not a hard rule. Spring Boot typically comes prepackaged with Hibernate as the default JPA provider.
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
```

### ORM (Object-Relational Mapping) Frameworks (Hibernate, EclipseLink)
ORM frameworks map Java Objects to database tables and Java fields to columns, so you don’t manually write SQL for every CRUD operation. Popular ORM frameworks include Hibernate and EclipseLink. They can:
- Automatically generate SQL (INSERT, UPDATE, SELECT, DELETE).
- Map results back into objects.
- Track changes (dirty checking).
- Handle relationships (@OneToMany, @ManyToOne, etc.).
- Manage cascading deletes/updates.
- Handle transactions.

### DDD Aggregates
a DDD pattern that groups one or more tightly related domain entities that must always be consistent together. Key Concepts:
- **Aggregate Root**: The main entity that controls access to the aggregate. All interactions go through it.
- **Consistency Boundary**: Changes to entities within the aggregate must maintain consistency.
- **Transactional Boundary**: Operations on the aggregate are atomic; either all succeed or none do.
```java
public class Order { // Aggregate Root
    private List<OrderItem> items; // Part of the aggregate
    public void addItem(Product p, int qty) {
        items.add(new OrderItem(p, qty));
    }
    public void removeItem(Product p) {     
        items.removeIf(item -> item.getProduct().equals(p));
    }
    public BigDecimal getTotal() {
        return items.stream()
                    .map(OrderItem::getSubtotal)
                    .reduce(BigDecimal.ZERO, BigDecimal::add);
    }
    public void processTransaction() {
        // All changes to Order and OrderItems are atomic
        PaymentService paymentService = new PaymentService();
        paymentService.chargePayment(items.getTotal());
    }
}
```

### Domain Repository
A design pattern that provides an abstraction layer for accessing and managing domain entities. Repositories encapsulate data access logic, allowing the domain layer to remain decoupled from the underlying data storage mechanism.
Domain Repositories must:
- Provide methods to add, remove, update, and query domain entities.
- Return domain entities, not DTOs or database models.
- operate on **aggregate roots**, not on child entities directly.
```java
// The OrderRepository interface defines methods to manage Order entities. 
// The interface prevents the domain layer from depending on specific data access implementations.
public interface OrderRepository {
    Order findById(Long id);
    void save(Order order);
    void delete(Order order);
}
```



### Context for all the above concepts:
User code → uses objects
Objects → have dependencies
Dependencies → created & injected by IoC Container
IoC Container → is ApplicationContext in Spring
ApplicationContext → creates beans, manages lifecycle
Beans → may be serialized → turned into byte streams
Byte streams → used for network/storage transfer
DTOs → objects specifically created to carry data across boundaries

### Byte Stream
A sequence of bytes(8 bit values) used for input/output (I/O) operations, such as reading from or writing to files, network sockets, or other data sources.
- Moves data between a program and the outside world.
- Allows universal input/output handling (files, network, memory, sockets).
- Enables serialization (objects → bytes → transport or storage).

They come and go from many sources:
- Files (FileOutputStream)
- Network connections (Socket.getOutputStream)
- Memory buffers (ByteArrayOutputStream)
- IPC channels (pipes)
- Caches, databases, messaging brokers

### Serialization & Deserialization
The process of converting an object into a **byte stream** for storage or transmission.
If a field is not serializable, it must be marked **transient** to avoid errors during serialization.
example:
```java
import java.io.Serializable;
public class Person implements Serializable {
    private static final long serialVersionUID = 1L;
    private String name;
    private int age;

}
// Serialization Example
ObjectOutputStream out = new ObjectOutputStream(new FileOutputStream("person.ser"));
out.writeObject(new Person("Alice", 30));
// Deserialization The process of converting a byte stream back into an object.
ObjectInputStream in = new ObjectInputStream(new FileInputStream("person.ser"));
Person p = (Person) in.readObject();
```

### Execution:
On Windows:
- mvnw.cmd spring-boot:run
- . ./Start.ps1 
- mvnw spring-boot:run
## Application Main Class
**@SpringBootApplication** is a **meta-annotation**. 
It autoconfigures everything needed for a typical application, based on:
- What libraries are in your Maven pom.xml
- What beans you have or haven’t defined
- Settings in application.properties or application.yml

This activates 3 three springboot features:
- @Configuration - "Use this class to configure"
- @EnableAutoConfiguration "Use a prebuilt configuration"
- @ComponentScan "Use existing components to choose prebuilt configuration"

The two core imports `org.springframework.boot(SpringApplication|autoconfigure)` import the core springboot framework, allowing you to use the main class as a configuration starting point.

*See autoconfiguration section for more details*

```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class DatacontrollerApplication {
	public static void main(String[] args) {
		SpringApplication.run(DatacontrollerApplication.class, args);
		// Run with 
	}
}
```
The application is executed by the JVM when this is ran in the main method.
```java
SpringApplication.run(DatacontrollerApplication.class, args);
```

## MVC Architecture
MVC = Model-View-Controller
Which is a design pattern for **server-rendered web applications**.
MVC often maintains:
- user sessions
- server-side state
- CSRF protection
- cookies bound to views
### Model
Your data and business logic.
Examples:
- domain objects
- service layer
- database entities
### View
HTML pages rendered by the server
This includes Thymeleaf, JSP(Java Server Page), JSPA (Java Server Page ADF)
### Controller
Coordinates the request → model → view.
Returns a view name that gets resolved to an HTML page.
#### Browser → Controller → Model → View(template) → Rendered HTML → Browser

### @Controller
**Meta-annotation** that designates a class as a Model-View-Controller.
This puts the html in the response body, **NOT** a json REST response.
```java
//This example returns the home html model with attributes added.
@Controller
public class HomeController {
    @GetMapping("/")
    public String home(Model model) {
        model.addAttribute("username", "Alice");
        return "index";  // maps to templates/index.html
    }
}
```
### Why MVC is outdated
Modern REST applications typically provide:
- REST API (Spring Boot REST)
- UI built in React, Angular, Vue, or mobile apps
- HTML rendering is moved to the client side, not the server.
- REST avoids: Template engines, view resolution, session creation.
- REST life cycle isn't a session but each request and response.
- MVC is for browsers, while REST is for any machine.
Examples of each architecture using **Spring Web MVC**:
```java
//REST //Rest gets you the web page independent of user, Client puts it together.
@RestController
@GetMapping("/profile")
public User getProfile() { return user; }
```
```java
//MVC //MVC shows the profile and builds it with the user. 
@Controller
@GetMapping("/profile")
public String showProfile() { return "profile"; }
```
Use @Controller + templates when:
- You want server-rendered HTML.
- You build a traditional web app.
- You need server-side UI logic.

Use @RestController when:
- You are building a REST API.
- You return JSON, not HTML.
- Your front-end is separate.
- You want stateless endpoints.



# REST
When an HTTP request hits a Spring Boot application:
```less
Request
    ↓
Servlet Container (Tomcat)
    ↓
Servlet Filter Chain (CORS filter, Security filters, Global filters)
    ↓
DispatcherServlet
    ↓
Handler Mapping (finds the @Controller method)
    ↓
Handler Adapter (invokes it)
    ↓
Response
```

## Request Mapping & Response Mapping
### @RequestMapping("/api")
defines the path and optionally the HTTP method for a controller or method.
It can be used:
- On classes (prefixes all methods)
- On methods (specific endpoints)
for example:
```java
//The below call would return user.
//https://somedomain.com/users POST
@RequestMapping(value = "/users", method = RequestMethod.POST)
public User createUser(@RequestBody User user) {
    return user;
}
```
### Both combined:

```java
GET /api/status 
@RestController
@RequestMapping("/api")
public class ApiController {
    @RequestMapping("/status")
    public String status() {
        return "OK";
    }
}
```

### Shortcuts
These are just convenience annotations wrapping @RequestMapping:
Shortcut	Equivalent to
- @GetMapping("/path")	@RequestMapping(value="/path", method=RequestMethod.GET)
- @PostMapping("/path")	RequestMethod.POST
- @PutMapping("/path")	RequestMethod.PUT
- @DeleteMapping("/path")	RequestMethod.DELETE

### Advanced Example:
```java
GET /api/v1/users/{id}b 
POST /api/v1/users
@RestController
@RequestMapping("/api/v1/users")
public class UserController {
    @GetMapping("/{id}")
    public User getUser(@PathVariable int id) {
        return userService.findById(id);
    }
    @PostMapping
    public User create(@RequestBody User user) {
        return userService.save(user);
    }
}
```
## Response 
in SpringBoot - **org.springframework.http** is the library that includes standardized responses to the request. 
### ResponseEntity
This is the ***HTTP Response class***, this controls the entire response including:
- **Headers - HttpHeaders**
- **Body - HttpBody**
- **Status Codes - HttpStatus**
### HttpStatus
An enum with each of the standard response codes:
```java
HttpStatus.OK              // 200
HttpStatus.CREATED         // 201
HttpStatus.BAD_REQUEST     // 400
HttpStatus.UNAUTHORIZED    // 401
HttpStatus.NOT_FOUND       // 404
HttpStatus.INTERNAL_SERVER_ERROR // 500
```
```java
//200 OK Response Example:
return new ResponseEntity<>(bodyText, HttpStatus.OK);
//Or
//201 CREATED
return ResponseEntity.status(HttpStatus.CREATED).body(newUser);
//OR Header + shortcut
return ResponseEntity.ok().header("X-Custom", "123").body(data);
// OR Spring Defaults headers and status code (ok 200) if you just return an object
@GetMapping("/user")
public User getUser() {
    return user;
}
//OR Customize the status to one not in the default enums(shortcuts)
@GetMapping("/user")
public ResponseEntity<User> getUser() {
    return ResponseEntity.status(HttpStatus.ACCEPTED).body(user);
}
//OR a custom status with no content
return ResponseEntity.noContent().build(); // 204 No Content
```
### @RestController = @Controller(class that conditionally passes data based on endpoints) + @ResponseBody(body of an html response) 
is a core pieces of the Spring Web MVC layer. It defines what the API is.
The rest controller will pass back the appropriate code base somehow with json.
It tells Spring: Do **NOT** return HTML templates. & Instead serialize method return values directly into the HTTP response (JSON/XML).
#### For Example: https://webdomain.com/hello GET
```java
@RestController
public class HelloController {
    @GetMapping("/hello")
    public String hello() {
        return '{
            "message" : "Hello World"
        }';
    }
}
```


### Headers Continued
There are 3 levels to controlling headers:
- Per-response headers (inside a controller, per endpoint)
- Global headers for every response (via Security, filters or **WebMvcConfigurer**)
- Conditional or dynamic headers (logic-based injection)
### Headers Summary
- Method	Scope	Best for
- ResponseEntity	Single endpoint	Custom headers per-API
- Filter (OncePerRequestFilter)	All responses	Global headers
- Interceptor	After controller	Request/response logic
- Spring Security headers	All responses	Security headers
```java
//customize all the headers you want this way, but specific to endpoint.
//Per-response
@GetMapping("/example")
public ResponseEntity<String> example() {
    return ResponseEntity
            .ok()
            .header("X-App-Version", "1.0")
            .header("Cache-Control", "no-store")
            .body("hello");
}
// Or Call the HttpHeaders explicitly
@GetMapping("/example2")
public ResponseEntity<String> example2() {
    HttpHeaders headers = new HttpHeaders();
    headers.add("X-Custom", "ABC");
    headers.add("X-Env", "DEV");
    return new ResponseEntity<>("data", headers, HttpStatus.OK);
}
//Or import jakarta servlets that handle many conditions by filters
import jakarta.servlet.FilterChain;
import jakarta.servlet.ServletException;
import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;
import org.springframework.stereotype.Component;
import org.springframework.web.filter.OncePerRequestFilter;

import java.io.IOException;

@Component
public class GlobalHeaderFilter extends OncePerRequestFilter {

    @Override
    protected void doFilterInternal(
            HttpServletRequest request,
            HttpServletResponse response,
            FilterChain filterChain) throws ServletException, IOException {

        response.addHeader("X-App-Name", "MyApp");
        response.addHeader("X-Author", "Human");
        response.addHeader("X-Powered-By", "Spring Boot");

        filterChain.doFilter(request, response);
    }
}
//Or you can use Application wide security headers with Spring Security
@Configuration
@EnableWebSecurity
public class SecurityConfig {
    @Bean
    SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
        http
            .headers()
                .xssProtection()
                .and()
                .contentSecurityPolicy("default-src 'self'");
        return http.build();
    }
}

```

## Servlet
Servlets are Java classes that handle HTTP requests and responses in web applications. They run inside a servlet container (like Tomcat) and provide low-level access to request/response data.
```java
// This simple servlet has been made obsolete by Spring MVC controllers
import jakarta.servlet.http.HttpServlet;
import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;
import java.io.IOException;

public class MyServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) 
            throws IOException {
        resp.getWriter().write("Hello world");
    }
}
```
The process might look like: `Tomcat → DispatcherServlet → Controllers → Response`

### HttpServletRequest
Represents the HTTP request received by the server. It provides methods to access everything in the request:
- URL 
- path
- query parameters
- headers
- cookies
- input body
- HTTP method
- content-type
- client IP
- session
```java
// Example of getting a header from the request
request.getHeader("Ip-Address");
// Example of getting the body as an InputStream
request.getInputStream();
```
### HttpServletResponse
Represents the HTTP response that the server sends back to the client. It provides methods to set:
- headers
- status code
- cookies
- content type
- response body
- output streams

### Spring MVC Toolkit Vs Low-Level Servlets
Even though Spring MVC gives you higher-level tools:
- @RequestParam
- @RequestBody
- @ResponseBody
- ResponseEntity
- @PathVariable
You can still access the low-level HttpServletRequest and HttpServletResponse objects directly in your controller methods if needed.
```java
response.addHeader("X-ID", "123"); // response.addHeader("X-ID", "123");
String body = request.getReader().lines().collect(Collectors.joining()); // reading a raw request body
OutputStream out = response.getOutputStream(); // writing raw bytes to response 
out.write(bytes);
response.addCookie(new Cookie("token", jwt));  // Setting a cookie
```

## Cross-domain Resource Sharing (CORS)
CORS is a browser security mechanism that controls whether a web page loaded from one origin is allowed to make HTTP requests to another origin.
Spring Boot implements CORS rules so your REST API can decide who is allowed to talk to it from the browser.

### Origin
An origin is defined by: **scheme** + **domain** + **port**
This is **browser-only** security. Servers do not enforce same-origin; browsers do.
In a setup like below if you load a frontend from Origin A, and it tries to call an API on Origin B, the browser blocks it unless CORS rules permit it.:
- https://app.example.com        → origin A
- https://api.example.com        → origin B  
- http://localhost:3000          → origin C
- http://localhost:8080          → origin D
### CORS config
To enable frontends running on **localhost:3000** (React, Vue, Angular). That have backends running on **localhost:8080** (Spring Boot). A browser will block the website from working without cors rules to allowing both origins.
#### CORS configuration tells Spring Boot:
- Which origins can call your API - (allowedOrigins)
- Which HTTP methods are allowed - (allowedMethods)
- Which custom headers can be sent - (allowedHeaders)
- Whether credentials/cookies are allowed - (allowCredentials)
- Which response headers should be visible to JS - (exposedHeaders)
```java
//CORS configurations apply to every controller.
//These add headers to all responses and tell the browser what cross origins to allow.
@Configuration
public class CorsConfig implements WebMvcConfigurer {
    @Override
    public void addCorsMappings(CorsRegistry registry) {
        registry.addMapping("/**")
                .allowedOrigins("*")
                .allowedHeaders("*")
                .allowedMethods("*")
                .exposedHeaders("X-My-Custom-Header");
    }
}

//Or Specific Origins allowed
@Configuration
public class CorsConfig implements WebMvcConfigurer {
    @Override
    public void addCorsMappings(CorsRegistry registry) {
        registry.addMapping("/**")
                .allowedOrigins("http://localhost:3000", "https://myapp.com")
                .allowedMethods("GET", "POST", "PUT", "DELETE")
                .allowedHeaders("*")
                .allowCredentials(true)
                .exposedHeaders("X-Custom-Header");
    }
}

//Or a per controller/endpoint option
//This says if it comes from localhost:3000 allow this response.
@CrossOrigin(origins = "http://localhost:3000")
@RestController
public class DemoController {
    @GetMapping("/data")
    public String data() {
        return "ok";
    }
}
```
## HttpSecurity
### HttpSecurity object
HttpSecurity is a Spring Security builder object. You use it inside a bean definition to customize web security. 
HttpSecurity is used to configure:
- HTTPs by default
- which URLs require authentication
- what kind of authentication to use
- login/logout behavior
- CSRF settings
- CORS rules
- security headers
- filters
- session rules
```java
@Bean
public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
    http.csrf().disable().authorizeHttpRequests(auth -> auth
            .requestMatchers("/public/**").permitAll()
            .anyRequest().authenticated()
        )
        .formLogin()
        .and()
        .httpBasic();
    return http.build();
}
```

### SecurityFilterChain
SecurityFilterChain is the final assembled chain of security filters created from your HttpSecurity configuration. The chain processes **every incoming HTTP request** ***BEFORE*** it reaches your **controllers**.
- Single Chain (typical Spring setup)
- Muti Chain (Advanced setup)
**SecurityFilterChain** contains filters such as:
- UsernamePasswordAuthenticationFilter
- BasicAuthenticationFilter
- CsrfFilter
- CorsFilter
- SessionManagementFilter
- AuthorizationFilter
```java
// This turns the instructions into a SecurityFilterChain
return http.build();
```
Spring Security added to the classpath provides:
- CSRF protection
- strong password encoding
- session management
- Clickjacking/XSS headers
- HTTPS redirection
- every endpoint becomes protected
- you explicitly open only what you want

You can use all sorts of authentication types like:
- JWT tokens
- OAuth2 (Google, GitHub, Keycloak)
- API keys
- Custom filters
```java
//For example you want to use a json web token
http.addFilterBefore(jwtFilter, UsernamePasswordAuthenticationFilter.class);
```
#### Multiple Security Patterns
If you need different rules for different URL patterns :
```java
// One set of security for the apiChain
@Bean
SecurityFilterChain apiChain(HttpSecurity http) throws Exception {
    http.securityMatcher("/api/**")
        .authorizeHttpRequests(auth -> auth.anyRequest().authenticated())
        .httpBasic();
    return http.build();
}
// A different set for the root
@Bean
SecurityFilterChain webChain(HttpSecurity http) throws Exception {
    http
        .securityMatcher("/**")
        .authorizeHttpRequests(auth -> auth.anyRequest().permitAll());
    return http.build();
}
```



## JavaBean Vs SpringBean
Inside Spring, a bean is any object that Spring creates, configures, and manages in the **application context container**.

However a Spring Bean is a managed object in the Spring IoC container.
***They are unrelated concepts except that many Spring Beans are implemented as JavaBeans***
### JavaBean Convention
JavaBeans are typically used as data carriers (POJOs).

JavaBeans are java objects that follow a design pattern:
1. It has a **public no-argument constructor**.
2. It has **private fields**.
3. It exposes those fields through **public getters and setters**.
4. It’s **serializable** (optional in modern usage but part of the original spec).
```java
public class User {
    private String name;
    private int age;

    public User() {} // no-arg constructor

    public String getName() { return name; } // getter
    public void setName(String name) { this.name = name; } // setter

    public int getAge() { return age; } // getter
    public void setAge(int age) { this.age = age; } // setter
}
```
### Spring Bean
Again, a Spring Bean is a managed object in the Spring IoC container. It can include:
- Services
- Controllers
- Repositories
- Configuration classes
- Utility components
- Anything else Spring constructs for you

### @Bean
is a **Spring meta-annotation** used inside a **@Configuration** class to tell Spring:
Create this object and register it in the application context as a Spring bean.

Spring @Bean is used on methods not classes like a JavaBean.

```java
// Note how AppConfig is the object, it's using a different custom object DataSource
// In this context the Spring bean dataSource() is using the JavaBean DataSource
@Configuration
public class AppConfig {
    @Bean
    public DataSource dataSource() {
        HikariDataSource ds = new HikariDataSource();
        ds.setJdbcUrl("jdbc:postgresql://localhost:5432/mydb");
        ds.setUsername("user");
        ds.setPassword("pass");
        return ds;
    }
}
```

### Spring Bean Scopes
A spring bean scope defines how long a Spring bean lives and how many instances Spring creates.
1. Singleton (default) Bean
   - One instance per application context.
   - Created at startup, reused everywhere.
   - Most common for services.
```java
@Service // default = singleton
public class UserService { }
```
2. Prototype Bean
   - New instance every time requested.
   - Not managed after creation.
```java
@Scope("prototype")
@Component
public class ReportGenerator { }
```
3. Request Bean
   - One instance per HTTP request.
   - Used in web controllers & filters.
```java
@Scope("request")
@Component
public class RequestScopedBean { }
```
4. Session (Web)
   - One instance per HTTP session.
5. Application (Web)
   - One instance for the entire servlet context (similar to singleton but tied to web app container).

#### The Bean Life cycle is:
1. Instantiation
- Spring calls the constructor (or factory method).
2. Dependency Injection
- Spring injects constructor args, setters, or fields.
3. Aware Interfaces (optional)
If a bean implements certain interfaces, Spring injects framework metadata:
- BeanNameAware → gives bean's name
- ApplicationContextAware → injects context
- EnvironmentAware, etc.
4. Bean Post-Processors (before init)
- BeanPostProcessor#postProcessBeforeInitialization runs.
- Used for things like:
- @Autowired processing
- Validation
- Proxy creation (AOP, @Transactional)
5. Initialization
One of these may run:
- A method annotated with @PostConstruct
- A method named in @Bean(initMethod = "methodName")
- Implementing InitializingBean#afterPropertiesSet()
6. Bean Post-Processors (after init)
BeanPostProcessor#postProcessAfterInitialization
Spring may wrap the bean with a proxy (AOP, transactional behavior).
7. Bean is ready for use
8. Destruction (only for singleton + request/session/application)
When the context shuts down, Spring calls:
- @PreDestroy
- or a destroy method in @Bean(destroyMethod = "...")
- or DisposableBean#destroy()

## Template Engines
are server-side HTML template engines used when you want your Spring Boot application to render HTML pages, not just JSON. When Spring detects a template engine it sets auto configured protocols.
Then it looks for traditional webpage files like html in **src/main/resources/templates**
Templates are traditionally used for simple pages and ***not used with rest APIs*** like:
- Traditional MVC web pages
- Admin dashboards
- Forms
- Custom UI without a front-end SPA

## AutoConfigurations
Each auto-configuration class uses conditional annotations such as:
- @ConditionalOnClass
- @ConditionalOnMissingBean
- @ConditionalOnProperty
- @ConditionalOnResource

For Example: 
```java
@ConditionalOnClass(DataSource.class)
@ConditionalOnMissingBean(DataSource.class)
public class DataSourceAutoConfiguration {
    // creates a HikariCP DataSource if none exists
}
```
Every Prebuilt configuration has different triggers to load the dependencies and settings. Some examples include:
#### Web
If Spring MVC is on classpath:
- DispatcherServlet
- Jackson JSON converters
- Message converters
- Static resource handling
- Tomcat/Jetty/Netty embedded server

#### Data
If Spring Data + JDBC/JPA are present:
- DataSource
- Connection pooling (HikariCP)
- EntityManagerFactory
- TransactionManager
- Hibernate JPA settings

#### Database Clients
If detected:
- JDBC (DriverManager)
- HikariCP pool
- Liquibase/Flyway migration support
- MongoDB client
- Redis template/connection
- Cassandra session

#### Security
If Spring Security is present:
- Filters
- Password encoders
- Default security config (login page, CSRF, etc.)

#### Actuator
If actuator is on classpath:
- Health endpoints
- Metrics
- Info endpoint

#### Messaging
If libraries are found:
- KafkaTemplate
- RabbitTemplate
- JMS connection factories
#### Templates
If Thymeleaf/Freemarker/Mustache on classpath:
- Template resolvers
- View resolvers
#### Logging
- Always auto-configured:
- Logback setup
- Log formatters
- Logging levels from properties
  
### Logging
Spring Boot always sets up logging, even in pure REST or CLI apps.
#### **Logback** is the default in SpringBoot
Spring loads 
```java
classpath:logback-spring.xml
//Logback example of boot up
2025-12-03 22:01:21 INFO 12345 --- [  main] com.example.App : Starting App
```
More settings can be found in **application.properties** like:
- logging.level.root=INFO
- logging.level.org.springframework=DEBUG
- logging.file.name=app.log



