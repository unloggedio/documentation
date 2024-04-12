# Generating JUnit Tests with Unlogged

With Unlogged.io, you have the capability to automatically convert recordings of code execution into JUnit tests. This innovative feature is designed to streamline the testing process, making it more efficient and effective.

## How Does It Work?
Unlogged.io meticulously tracks the execution of your code as it runs. This tracking captures all the necessary details of the code’s behavior and outputs. Following the completion of code execution, Unlogged utilizes this detailed recording to generate JUnit tests. 

**These tests reflect the recorded execution path and outcomes, emulating real world scenarios.**

![](assets/images/junit.gif)

!!! tip Utilizing Boilerplate Generation
    If generating JUnit tests post-execution does not align with your workflow, or if you prefer to set up tests in advance, Unlogged.io offers a boilerplate generation option. This feature allows you to create template-based tests before running your actual code. 

## How's this different from co-pilot and AI generated tests?

Unlogged.io stands out in the Java development tools space with several unique features. We offer runtime mocking, performance tracking, and real-time visual code coverage, which are not commonly available in similar products. 

Additionally, Unlogged offers specific capabilities for handling real-world data and scenarios, providing developers with tools to test and refine code under realistic conditions. 

| Features                          | Unlogged   | Co-Pilot  | diffblue   | sapient ai | codium AI  | IntelliJ AI |
|-----------------------------------|------------|-----------|------------|------------|------------|-------------|
| Runtime mocking                   | <span style="color:green">Yes</span> | <span style="color:red">No</span> | <span style="color:red">No</span> | <span style="color:red">No</span> | <span style="color:red">No</span> | <span style="color:red">No</span> |
| Bulk JUnit Test Generation        | <span style="color:green">Yes</span> | <span style="color:green">Yes</span> | <span style="color:green">Yes</span> | <span style="color:green">Yes</span> | <span style="color:green">Yes</span> | <span style="color:green">Yes</span> |
| Performance Tracking              | <span style="color:green">Yes</span> | <span style="color:red">No</span> | <span style="color:red">No</span> | <span style="color:red">No</span> | <span style="color:red">No</span> | <span style="color:red">No</span> |
| No Code Tests                     | <span style="color:green">Yes</span> | <span style="color:red">No</span> | <span style="color:green">Yes</span> | <span style="color:green">Yes</span> | <span style="color:green">Yes</span> | <span style="color:red">No</span> |
| Code Generation using AI          | <span style="color:red">No</span> | <span style="color:green">Yes</span> | <span style="color:red">No</span> | <span style="color:red">No</span> | <span style="color:red">No</span> | <span style="color:green">Yes</span> |
| Real World Data/Scenarios         | <span style="color:green">Yes</span> | <span style="color:red">No</span> | <span style="color:red">No</span> | <span style="color:red">No</span> | <span style="color:red">No</span> | <span style="color:red">No</span> |
| Real Time Visual Code Coverage    | <span style="color:green">Yes</span> | <span style="color:red">No</span> | <span style="color:red">No</span> | <span style="color:red">No</span> | <span style="color:red">No</span> | <span style="color:red">No</span> |
| PR Documentation                  | <span style="color:red">No</span> | <span style="color:green">Yes</span> | <span style="color:red">No</span> | <span style="color:red">No</span> | <span style="color:red">No</span> | <span style="color:green">Yes</span> |
| Convert from one Language to another | <span style="color:red">No</span> | <span style="color:red">No</span> | <span style="color:green">Yes</span> | <span style="color:red">No</span> | <span style="color:red">No</span> | <span style="color:green">Yes</span> |



