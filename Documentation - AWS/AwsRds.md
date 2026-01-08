# My Notes

### Connecting to AWS Services with Java SDK
To connect to AWS services using the Java SDK, ensure you have the AWS SDK for Java included in your project dependencies. You can use Maven or Gradle for dependency management.
### Example: Connecting to RDS
Here's a simple example of how to connect to an Amazon RDS instance using the AWS SDK for Java:

### Configurations
Once you have the dependencies, you must configure your application's connection properties in your application.properties (or application.yml) file. This configuration is the same whether the database is on AWS RDS or a local server; Spring Boot uses the standard properties

```java
spring.datasource.url=jdbc:postgresql://<rds-instance-endpoint>:<port>/<database-name>
spring.datasource.username=<your-username>
spring.datasource.password=<your-password>
spring.jpa.hibernate.ddl-auto=update # Recommended for development, change to 'validate' or 'none' for production
spring.jpa.show-sql=true # Optional: shows SQL queries in the console
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.PostgreSQLDialect
```