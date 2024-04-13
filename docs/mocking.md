# Mocking

Traditionally, developers set up wiremock to mock APIs, and test containers to mock downstream services or database/redis calls. 

With one click, Unlogged lets you mock :material-api:{ .heart }API, :material-database:{ .heart }DB, :material-arrow-down:{ .heart }downstream service calls 

and :file_folder:{ .heart }file operations, in runtime. 

## Recorded Mocks

Unlogged automatically identifies the lines of code that can be mocked. 


:simple-ghostery:{ .heart } A ghost icon will appear next to the identified lines. 

Use postman/swagger or Direct Invoke and the unlogged will show you the mocks with recorded ```when``` and ```then``` values. 

![](assets/images/mockingfinal.gif)

## Choices of Mock Execution

Unlogged provides developers with a versatile mocking feature that allows for three distinct behaviors when handling method returns within tests. You can set a mock to execute its normal behavior, return a null value, or throw a designated exception. This flexibility supports various testing scenarios, enabling developers to thoroughly test software behavior under different conditions.

## What happens underneath when you mock?

The plugin informs the sdk to replace the line of code with its mocks. In rutime, the mocks get executed instead of actual code. 

!!! tip
	The mock gets executed when you call the method either from Postman/Swagger or Direct Invoke. 

!!! failure "Static or Same Class methods"
	Note that the static methods or methods within the same class **can't be mocked**. You will **NOT** see the ghost :simple-ghostery:{ .heart } icon in such cases.
