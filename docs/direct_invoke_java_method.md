# Call Java Methods Directly

To test a ```java``` method, traditionally, you either have to write a unit test, or expose an http end point and then ```F8```/step over :material-debug-step-over:{ .heart } till you reach your method. A few folks often use ```System.out.print``` to debug. 

We connect a lot with this meme from [monkeyuser](https://www.monkeyuser.com/2017/step-by-step-debugging/)

![](assets/images/debugging.png) 

## Direct Invoke 

With ```Direct Invoke``` you can call a Java method directly. Once you start your application in debug mode, you will see the cyan colored icon next to any method. Click on it and Unlogged pre-fills it with dummy arguments. Execute the method and you will get the return value just for the method you called.

![](assets/images/diwithdebug.gif)

## Debug where it matters

Start debugging where it matters. Put a breakpoint anywhere in the method and execute a method using ```Direct Invoke```. Check IntelliJ's debugger and values of all variables.

No need to expose an http end point or write a unit test to debug something deep within your code.

!!! warning
    DO NOT call your ```main``` method using ```Direct Invoke``` It will fail since it attempts to start the process again using Unlogged with the same ports.

## What can you do with a replay?

1. **Save and Push to Git**: The replays are saved in the form of a json, inside your repository. You can push them to git and collaborate with your team memebers.
2. **Run them in CI**: A simple ```mvn test``` or ```./gradlew test``` replays all replay tests. 
3. **Get Code Coverage Report**: Use surefire or any other reporting plugin to get code coverage reports with our replay tests.
4. **Maintain no extra code**: Replays are saved in the form of a json and no extra generated code is added to your repository.

!!! tip
    The replay tests automatically pick up the necessary mocks. 
