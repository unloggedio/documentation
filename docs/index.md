# Getting Started

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
      <version>0.1.12</version>
    </dependency>
    ```

=== "gradle"
    ``` groovy
    dependencies
    {
        implementation 'video.bug:unlogged-sdk:0.1.12'
        annotationProcessor 'video.bug:unlogged-sdk:0.1.12'
    }
    ```

Sync your project once so that the Unlogged dependency is downloaded from maven repository.

### Adding the annotion
To start recording method input and return values - add ```@Unlogged``` annoation just above your main method.

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