# Guttor Icons & What they mean

For every method in your code base, you will see different guttor icons. 

The below chart explains what these guttor icons mean and what you are expected to do.


#### Application Not Running with Unlogged

This icon means that your application is not running with Unlogged. You can add the Unlogged dependency in your pom.xml or build.gradle, mvn clean package or gradle clean build and start debugging your application.

#### Application Running with Unlogged

Once you see this icon, it means that your application is running with Unlogged. Now, you can invoke any method inside your Java code using Direct Invoke or call http end points using Postman, Swagger or UI.

#### Recording Available for methods

Once you execute a method, using either Direct Invoke, Postman, or Swagger, you will see this icon. It indicates that the method has the recorded data in the form of input and return values. 

#### Execute Method

If you make code changes after a recording is done for a method, you will see a bolt icon. That means you can now hot-relaod the method and replay its previously recorded inputs.

#### Passing Case

After your code changes, and once you execute the method, this icon tells you if the return value is same as before. 

#### Failing Case

After your code changes, and once you execute the method, this icon tells you if the return value is different from before. 