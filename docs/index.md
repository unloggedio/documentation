# Getting Started

Welcome to Unlogged, the secret weapon designed specifically for Java developers seeking to consistently produce reliable and high-performing code.

With Unlogged-SDK integrated into your Java applications, you gain unparalleled insights into your application's runtime behavior and unlock a plethora of new capabilities.

## Real-Time Insights

- Gain timed traces of all executed methods
- Access return values for every method call
- Monitor time spent on each line of code
- Live coverage tracking for comprehensive analysis

Experience the power of live insights:
![](assets/images/liveview.gif)

## Revolutionary Capabilities

### Live Mocking

Effortlessly mock any downstream call within your running application. Our "Always Available" live mocking feature eliminates the need for containers or services, allowing seamless integration into your development workflow. Save mock definitions as JSON files, ensuring consistency across your team.

[Live View](https://read.unlogged.io/liveview/)

Witness live mocking in action:
![](assets/images/mockingfinal.gif)

### Replay Tests

Capture application traffic as replay tests and seamlessly trigger them within your CI pipeline using mvn test. Ensure the reliability of idempotent methods and safeguard against regressions.

[Replays](https://read.unlogged.io/replays/)

- Unit replay tests: leverage custom mocks for precise testing
- Integration replay tests: validate end-to-end functionality
- Failure replay tests: fortify failing cases to ensure consistent results

Watch how to create and manage replay tests:
![](assets/images/loadingreplays.gif)

### Automated Test Generation

[Test Generation](https://read.unlogged.io/saveandrun/)

Automate test script generation with JUnit, utilizing replay tests or generating boilerplate code to kickstart your testing efforts. Seamlessly integrate with Mockito for efficient test dependency management.

Unlock the potential of automated testing with Unlogged, streamlining your development process and ensuring the reliability and performance of your Java applications.

Install Unlogged, record and replay java methods, track code coverage, mock external and downstream calls, and create perfectly working JUnit tests. 

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
      <version>0.3.9</version>
    </dependency>
    ```

=== "gradle"
    ``` groovy
    dependencies
    {
        implementation 'video.bug:unlogged-sdk:0.3.9'
        annotationProcessor 'video.bug:unlogged-sdk:0.3.9'
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
    Unlogged adds probes in your code and causes noticeable performance degradation. We are working on a **production-deployable** version and will keep our documentation updated accordingly.

### Disabling Unlogged

You can disable unlogged either in compile or runtime.

#### Compile Time

=== "maven"
    ``` maven
    mvn package -Dunlogged.disable
    ```

=== "gradle"
    ``` groovy
    ./gradlew build -Dunlogged.disable
    ```

#### Run Time

Update the ```annotation``` on top of your main method.

``` Java
@Unlogged(enable = false)
```

!!!tip "Remember" 

    Note that when you disable the annotation in runtime, the logging probes are still added to your code. But they won't log anything, since the ```enable``` flag is set to ```false```