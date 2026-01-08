# SpringBoot

## Chapter 1  

### Spring Web

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

### Jackson Library\

The defacto standard for handling json in java apps

#### pom

```xml
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <!-- Use the latest version available, e.g., 2.19.0. 
         Check Maven Central for the most recent stable version. -->
    <version>2.19.0</version> 
</dependency>
```

```java
import com.fasterxml.jackson.databind.ObjectMapper;
ObjectMapper mapper = new ObjectMapper();

// Convert Java object to JSON string
String jsonString = mapper.writeValueAsString(myJavaObject);

// Convert JSON string to Java object
MyJavaObject obj = mapper.readValue(jsonString, MyJavaObject.class);
```
