# Running the Replay Tests in CI

While running the replay tests locally is important during development for rapid feedback, using a CI pipeline :material-sync:{ .heart } enhances the overall development process by automating the testing and validation steps in a controlled and scalable environment. It ensures that the codebase is reliable and meets quality standards before changes are pushed to production.

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

### Replays like unit tests

- mock all the dependency calls inside your methods 
- bind them with the replays. 

unlogged-sdk test runner uses the JUnit Platform test runner to run replays created using the plugin. To execute unlogged tests as ```mvn test``` or ```gradle test``` or ```intellij run test```.

Start by creating the following test class file ```UnloggedTest.java``` in your src/test/java directory

```java
	
import io.unlogged.runner.UnloggedTestRunner;
import org.junit.runner.RunWith;

@RunWith(UnloggedTestRunner.class)
public class UnloggedTest {

}
```

!!! tip
	Yep! This class has no methods since the replay tests will be based on ```src/test/resources/unlogged/<ClassName>.json``` files.

Execute ```mvn test``` or ```gradle test``` to execute the tests from CLI.
