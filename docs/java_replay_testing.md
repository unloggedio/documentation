# Saving and running the Replays

You can save the replays and git push them to your repo so that your team mates can start using the replay tests you created.

## Types of Replays

You can save and run the replays either in unit mode or integration mode. In unit mode, all the mocks inside a method are automatically saved and mapped with the replay.

In integration mode, no mocks are applied.

## Assertions

When you click on save, we save them with one on one key value assertions. You can edit them later from library.

## Mocks

All the mocks needed for the replays are stored and mapped automatically to the replays. 

Replays and mockd with assertions are saved at the below location

```/YOUR MODULE DIRECTORY/src/test/resources/unlogged```

![](assets/images/savereplay.gif)

## How to run the Replays in CI?

While running the replay tests locally is important during development for rapid feedback, using a CI pipeline :material-sync:{ .heart } enhances the overall development process by automating the testing and validation steps in a controlled and scalable environment. It ensures that the codebase is reliable and meets quality standards before changes are pushed to production.

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

### Replays like unit tests

Start by creating the following test class file ```UnloggedTest.java``` in your src/test/java directory

```java
    
import io.unlogged.runner.UnloggedTestRunner;
import org.junit.runner.RunWith;

@RunWith(UnloggedTestRunner.class)
public class UnloggedTest {

}
```

and then run this simple command.

=== "maven"
    ``` xml
    mvn test
    ```

=== "gradle"
    ``` groovy
    ./gradlew test
    ```

!!! tip
    Yep! This class has no methods since the replay tests will be based on ```src/test/resources/unlogged/<ClassName>.json``` files.

### Integration testing on Springboot application

For Springboot applications, customize the above tests as follows:

```java
@RunWith(UnloggedTestRunner.class)
@ComponentScan("<spring.application.package.name>")
@EnableAutoConfiguration
@PropertySource(
value = {"config/application.yml", "config/application-dev.yml"},
factory = UnloggedRunnerTest.YamlPropertySourceFactory.class) 
@TestPropertySource({"classpath:application.properties"})
@WebAppConfiguration
public class UnloggedRunnerTest {

    public static class YamlPropertySourceFactory implements PropertySourceFactory {
        public YamlPropertySourceFactory() {
        }

    @Override
    public PropertiesPropertySource createPropertySource(String name, EncodedResource encodedResource) throws IOException {
            YamlPropertiesFactoryBean factory = new YamlPropertiesFactoryBean();
            factory.setResources(encodedResource.getResource());
            return new PropertiesPropertySource(encodedResource.getResource().getFilename(), factory.getObject());
       }
    }
}
```

!!! example "Remember!"
    Remember to update ```<spring.application.package.name>``` to your package name, ```config/application-dev.yml``` to the config files you want to use. ```UnloggedRunnerTest.YamlPropertySourceFactory.class``` is for supporting yml files. Specify your test application properties inside ```ApplicationProperties.class```.

`WebAppConfiguration` annotation is needed if there are any methods in starting class of the project that configure services, that cannot be enabled for integration tests. For example some configuration for Swagger or API monitoring. If these configurations are in a seperate file, then the annotation is not needed.

With this, unlogged test runner will create as instance of the spring application context and execute the tests based on the beans created by spring.

### Code Coverage Reports for Replays

Running ```mvn test``` or ```gradle test``` will generate ```xml``` reports that are stored at ```${basedir}/target/surefire-reports```



