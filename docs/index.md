# Getting Started

Install Unlogged, record and replay ```java``` methods, track code coverage, mock external and downstream calls, and create perfectly working Junit tests. 

### Installing the Plugin

* IntelliJ IDEA --> Preferences --> Plugins --> Marketplace
* Search for Unlogged in the marketplace & Install

![](assets/images/1.png)

### Adding the dependency

=== "maven"
    ``` xml
    <dependency>
      <artifactId>unlogged-sdk</artifactId>
      <groupId>video.bug</groupId>
      <version>0.1.18</version>
    </dependency>
    ```

=== "gradle"
    ``` groovy
    dependencies
    {
        implementation 'video.bug:unlogged-sdk:0.1.18'
        annotationProcessor 'video.bug:unlogged-sdk:0.1.18'
    }
    ```

Sync your project once so that the Unlogged dependency is downloaded from maven repository.

### Adding the annotation
To start recording method input and return values - add ```@Unlogged``` annotation just above your main method.

Here is an example.

```java hl_lines="1"
   @Unlogged
   public static void main(String[] args) {
        SpringApplication.run(JwtDemoApplication.class, args);
    }
```

### Clean, and Debug!

=== "maven"
    ``` maven
    mvn clean
    ```

=== "gradle"
    ``` groovy
    gradle clean
    ```

Start your application in debug mode to call any java function directly.

!!!danger "DO NOT deploy Unlogged in production!"
    Unlogged adds probes in your code and causes significant performance degradation. We are working on a **production-deployable** version and will keep our documentation updated accordingly.