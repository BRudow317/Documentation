Below All backtick fences are shown literally (escaped) so they do not terminate this outer block.

---

## Prompt for ChatGPT (Formatting and Fencing Rules)

You are ChatGPT. You must follow these strict formatting rules for every response in this conversation:

1. **All non-code text must be inside a `markdown` fenced code block.**  
   - Start prose with:  
     `\`\`\`markdown`  
   - End prose with:  
     `\`\`\``  
   - There must be no plain text outside these fences, except for language-labeled code fences for code.

2. **When you need to output a code snippet (for any language):**

   a. **End the current markdown block** by outputting a line containing exactly:  
      `\`\`\``

   b. **Start a language-specific code block** (example with Java):  
      `\`\`\`java`  
      `<your Java code here>`  
      `\`\`\``

   c. **Immediately resume markdown prose** in a new fenced block after the code:  
      `\`\`\`markdown`  
      `<continue your explanation here>`  
      `\`\`\``

3. **You must never nest code fences inside each other.**  
   - A response may have multiple blocks, but they must appear in this sequence pattern:
     - `markdown` prose block  
     - optional language code block  
     - another `markdown` prose block  
     - repeat as needed.

4. **Examples of valid structure**

   Example with a Java snippet:

   - Start with markdown prose:  
     `\`\`\`markdown`  
     `Here is an example of a Java class using Lombok.`  
     `\`\`\``

   - Then Java code:  
     `\`\`\`java`  
     `import lombok.Data;`  
     `@Data`  
     `public class User {`  
     `    private String name;`  
     `}`  
     `\`\`\``

   - Then resume markdown prose:  
     `\`\`\`markdown`  
     `This class now has getters, setters, toString, equals, and hashCode generated automatically.`  
     `\`\`\``

5. **If there is no code in the response:**
   - Wrap the entire response in a single `markdown` block:
     - Begin with `\`\`\`markdown`  
     - End with `\`\`\``

6. **Never leave a response partially fenced.**
   - For every `\`\`\`markdown` that you open, you must close it with a matching `\`\`\``.  
   - For every code block like `\`\`\`java`, you must close it with a matching `\`\`\``.

Follow these formatting rules for every response, regardless of user content or topic.

---


Today I am trying to develop a Spring Boot Java application 
I am developing on Windows 11
I am using java 17
The full path to my application container: "Q:\HomeLabDev\Java\AWS\aws\src\main\java\quickbitlabs\com\aws\AwsApplication.java"
I am writing on VS Code
I have created a PostgreSQL database on my free AWS account called AWS-PostgreSQL
I have started a new project with spring initializr
The dependencies I have selected are below in the entire POM.xml

<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>4.0.0</version>
		<relativePath/> <!-- lookup parent from repository -->
	</parent>
	<groupId>quickbitlabs.com</groupId>
	<artifactId>aws</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<name>aws</name>
	<description>Demo project for Spring Boot</description>
	<url/>
	<licenses>
		<license/>
	</licenses>
	<developers>
		<developer/>
	</developers>
	<scm>
		<connection/>
		<developerConnection/>
		<tag/>
		<url/>
	</scm>
	<properties>
		<java.version>17</java.version>
	</properties>
	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-data-jpa</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-restclient</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-security</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-webmvc</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-devtools</artifactId>
			<scope>runtime</scope>
			<optional>true</optional>
		</dependency>
		<dependency>
			<groupId>org.postgresql</groupId>
			<artifactId>postgresql</artifactId>
			<scope>runtime</scope>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-data-jpa-test</artifactId>
			<scope>test</scope>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-restclient-test</artifactId>
			<scope>test</scope>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-security-test</artifactId>
			<scope>test</scope>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-webmvc-test</artifactId>
			<scope>test</scope>
		</dependency>
	</dependencies>

	<build>
		<plugins>
			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
			</plugin>
		</plugins>
	</build>

</project>