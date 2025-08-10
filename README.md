
###  Automating Java Web-App Builds with Maven

Building modern Java applications involves more than just writing code — you need to manage dependencies, automate builds, run tests, generate coverage reports, and deploy efficiently.
![maven](https://media.geeksforgeeks.org/wp-content/uploads/20240612170604/Maven-Build-Life-Cycle.png)

We explore how Maven simplifies this using a Java Web application project as a practical example:

### Real-World Problem Statement: 
Organizations often struggle with creating scalable, modular, and maintainable web applications that integrate security, persistence, and automated deployment into a single workflow.

This project helps solve this by showing how a real Java web-app can be built using tools like Spring for structure and security, Hibernate to connect with a database, MySQL to store data, and Jetty to run the app locally — **all controlled and automated by Maven**. 

> Think of it like a recipe that builds, tests, and packages an app step-by-step — just like in the real world. That is Maven!


## Tech Stack


|Category| Technology| 
| -- | -- |
| Web Framework | Spring MVC, Spring Security|
|Persistence & ORM | Hibernate, Spring Data JPA, MySQL|
|Build & Dependency | Maven |
| Web Server (Dev)| Jetty (via plugin)|
|Testing Frameworks | JUnit, Mockito, Hamcrest|
| Logging | Logback | 
|Code Quality | JaCoCo |


> **Maven**: Automate builds and manage libraries, regardless of microservice architecture

## Software Requirements
- Java 8
- Maven 3.5+

---
## Code Overview
This project uses **Apache Maven** to manage build, testing, packaging, and dependencies. Below is a structured breakdown of the `pom.xml` file:

### Code & Workflow

1. `validate`: Checks if the project’s structure and pom.xml are correct.
```xml
<groupId>com.visualpathit</groupId>
<artifactId>vprofile</artifactId>
<version>v1</version>
<packaging>war</packaging>
```
2. `compile`: Compiles Java Source-code
> Dependencies for compilation:
```xml
<dependency>
  <groupId>org.springframework</groupId>
  <artifactId>spring-webmvc</artifactId>
</dependency>
<dependency>
  <groupId>org.hibernate</groupId>
  <artifactId>hibernate-entitymanager</artifactId>
</dependency>
```
3. `test`: Runs unit tests using the test libraries.
```xml
<dependency>
  <groupId>junit</groupId>
  <artifactId>junit</artifactId>
  <scope>test</scope>
</dependency>
<dependency>
  <groupId>org.mockito</groupId>
  <artifactId>mockito-core</artifactId>
</dependency>
```
 **Run**: mvn test 

4. `package`: Packs the compiled code into a `.war` file for deployment.
**Run**: mvn package
>Output file: `target/vprofile.war`

5. `verify`: Generates test coverage reports post integration testing.
```xml
<plugin>
  <groupId>org.jacoco</groupId>
  <artifactId>jacoco-maven-plugin</artifactId>
</plugin>
```
**Run**: mvn verify

6. `install`: Installs the `.war` in your local Maven repository for reuse.
>**Run**: mvn install 

7. `Jetty plugin`: to serve app locally
```xml
<plugin>
  <groupId>org.eclipse.jetty</groupId>
  <artifactId>jetty-maven-plugin</artifactId>
</plugin>
```
>**Run**: mvn jetty:run

>This setup allows access to localhost (http://localhost:8080/)
---

## Run Locally

1. Clone the project

```bash
  git clone https://github.com/TheSoloScientist/Maven
```

2. Go to the project directory

```bash
  cd vprofile
```

3. Install dependencies

```bash
  mvn clean install
```
4. Start the server

```bash
 mvn jetty:run
```
> **Open Browser**: http://localhost:8080/

## AWS Deployment Using Virtual Machines (EC2)
1. Create EC2 Instance
Choose Amazon Linux 2 or Ubuntu
Open ports: 22 (SSH), 8080 (App), 80 (HTTP) in security group

2. Install Required Software
```bash
sudo apt install git java-1.8.0-openjdk maven -y
```
> For Ubuntu AMI
3.  Clone and Run Project
```bash
git clone https://github.com/TheSoloScientist/Maven
```
cd vprofile
mvn clean package
mvn jetty:run
```
4. Access the App
```bash
Visit: http://<EC2_PUBLIC_IP>:8080/ 
```
## Demo
Here are the screenshots to follow-along:
---
Create an EC2 instance
![Demo Screenshot](https://github.com/TheSoloScientist/Maven/blob/main/demo.png/ec2.png)

---
Install Java-version dependencies
![Demo Screenshot](https://github.com/TheSoloScientist/Maven/blob/main/demo.png/jdk.png)

---
Install maven:
![Demo Screenshot](https://github.com/TheSoloScientist/Maven/blob/main/demo.png/mvn.png)

**Run**: mvn test
![Demo Screenshot](https://github.com/TheSoloScientist/Maven/blob/main/demo.png/test.png)

![Demo Screenshot](https://github.com/TheSoloScientist/Maven/blob/main/demo.png/final.png)
---

## Lessons Learned

What did you learn while building this project? What challenges did you face and how did you overcome them?

This Maven-powered project illustrates how to:
- Automate Java build workflows
- Use a modular dependency setup
- Execute local deployment with Jetty
- Integrate quality gates like JaCoCo test coverage
- Prepare a .war file suitable for production
With this **pom.xml**, testing and delivering features faster using automation built into Maven.

# Challenges
SSH is timing out on an IP (port 22), which confirms the issue is network-related.
- Try Connecting via EC2 Instance Connect
If this works, then:
Your local network is likely blocking outbound port 22 (e.g., school, work Wi-Fi)

Slow on local network
- Use a cloud service
This setup will **always** be fastest on a cloud platform internet.

## Acknowledgements

 - [ Readme Templates](https://awesomeopensource.com/project/elangosundar/awesome-README-templates)
- [ Maven setup ](https://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html#Build_Lifecycle_Basics)
- [Examples](https://www.geeksforgeeks.org/advance-java/maven-build-lifecycle/)
- [Source code](https://github.com/hkhcoder/vprofile-project/blob/local/pom.xml)
- [AWS setup](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/concepts.html)
