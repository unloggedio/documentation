# Running the Replay Tests in CI

While running the replay tests locally is important during development for rapid feedback, using a CI pipeline :material-sync:{ .heart } enhances the overall development process by automating the testing and validation steps in a controlled and scalable environment. It ensures that the codebase is reliable and meets quality standards before changes are pushed to production.

### Adding the dependency

=== "maven"
    ``` xml
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <scope>test</scope>
    </dependency>
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
        testImplementation 'org.junit.jupiter:junit-jupiter-api:{version}'
        testRuntimeOnly 'org.junit.jupiter:junit-jupiter-engine:{version}'
        implementation 'video.bug:unlogged-sdk:0.1.18'
        annotationProcessor 'video.bug:unlogged-sdk:0.1.18'
    }
    ```

### Replays like unit tests

- mock all the dependency calls inside your methods 
- bind them with the replays. 

The `unlogged-sdk` test runner uses the JUnit Platform test runner to run replays created using the plugin.

Start by creating the following test class file `UnloggedTest.java` in your `src/test/java` directory

```java
	
import io.unlogged.runner.UnloggedTestRunner;
import org.junit.runner.RunWith;

@RunWith(UnloggedTestRunner.class)
public class UnloggedTest {

}
```

!!! tip
	Yep! This class has no methods since the replay tests will be based on `src/test/resources/unlogged/<ClassName>.json` files.

Execute `mvn test` or `gradle test` or `intellij run test`  to run the tests from CLI.

### Integration testing on Springboot application

For Springboot applications, customize the above tests as follows:

```java
@RunWith(UnloggedTestRunner.class)
@ComponentScan("<spring.application.package.name>")
@EnableAutoConfiguration
@PropertySource(
value = {"config/application.yml", "config/application-dev.yml"},
factory = UnloggedRunnerTest.YamlPropertySourceFactory.class) 
@EnableConfigurationProperties({ApplicationProperties.class})
@TestConfiguration
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
	Remember to update `<spring.application.package.name>` to your package name, `config/application-dev.yml` to the config files you want to use. `UnloggedRunnerTest.YamlPropertySourceFactory.class` is for supporting yml files. Specify your test application properties inside `ApplicationProperties.class`.

With this, unlogged test runner will create as instance of the spring application context and execute the tests based on the beans created by spring.

### Reports

Running `mvn test` or `gradle test` will generate `xml` reports that are stored at `${basedir}/target/surefire-reports`

