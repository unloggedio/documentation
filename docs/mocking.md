# Mocking

With one click, Unlogged lets you mock API, DB, downstream service calls and file operations.

## Using Recorded Data

Unlogged automatically identifies the lines of code that can be mocked. 


![](assets/images/ghost.svg){ .heart } A ghost icon will appear next to the identified lines. 

Click on the ghost icon, and define the ```when``` condition and the corresponding```then``` return value, and click save. This will change the code in runtime and replace this line of code with the mock you just defined.

![](assets/images/mocking.gif)

## Mock as you write!

When you write a line of code, we automatically detect if the logic in the line can be mocked. 

You can click on the icon and define the mock, manually.

## Permanent Mocks

If you want to test only your application using APIs or UI, you can enable the permanent mocks. With this check, even when your method is accessed using an API call, the permanently mocked line will be mocked.

This is helpful while testing your method outside of ```Direct Invoke```, using Postman, or Swagger or your application UI.

![](assets/images/permocking.gif)
