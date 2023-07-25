# Getting Started

### Installing the Plugin

* IntelliJ IDEA --> Preferences --> Plugins --> Marketplace
* Search for Unlogged in the marketplace & Install

![Image title](assets/images/1.png)

### Adding the dependency

=== "maven"
    ``` xml
    <dependency>
      <artifactId>unlogged-sdk</artifactId>
      <groupId>video.bug</groupId>
      <version>0.0.14</version>
    </dependency>
    ```

=== "gradle"
    ``` groovy
    dependencies
    {
        implementation 'video.bug:unlogged-sdk:0.0.14'
        annotationProcessor 'video.bug:unlogged-sdk:0.0.14'
    }
    ```

### Adding the annotion
To start recording method input and return values - add ```@Unlogged``` annoation just above your main method.

Here is an example.

```java hl_lines="1"
   @Unlogged
   public static void main(String[] args) {
        SpringApplication.run(JwtDemoApplication.class, args);
    }
```

### Clean, and Run!

=== "maven"
    ``` maven
    mvn clean
    ```

=== "gradle"
    ``` groovy
    gradle clean
    ```