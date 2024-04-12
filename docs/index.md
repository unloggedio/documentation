# Unlogged Java Tool

Use Unlogged-SDK with your Java applications and gain unparalleled insights into your application runtime behavior and unlock a plethora of new capabilities.

## [Live view](liveview/)

- Gain timed traces of all executed methods
- Access return values for every method call
- Monitor time spent on each line of code
- Live coverage tracking for comprehensive analysis

![](assets/images/liveview.gif)


## [Real time call mocking](mocking/)

Effortlessly mock any downstream call within your running application. Our "Always Available" live mocking feature eliminates the need for containers or services, allowing seamless integration into your development workflow. Save mock definitions as JSON files, ensuring consistency across your team.


![](assets/images/mockingfinal.gif)

## [Replay testing](java_replay_testing/)

Capture application traffic as replay tests and seamlessly trigger them within your CI pipeline using mvn test. Ensure the reliability of idempotent methods and safeguard against regressions.

- Unit replay tests: leverage custom mocks for precise testing
- Integration replay tests: validate end-to-end functionality
- Failure replay tests: fortify failing cases to ensure consistent results

![](assets/images/loadingreplays.gif)

## [Automated JUnit Test generation](generate_automated_junit/)

Automate test script generation with JUnit, utilizing replay tests or generating boilerplate code to kickstart your testing efforts. Seamlessly integrate with Mockito for efficient test dependency management.

Unlock the potential of automated testing with Unlogged, streamlining your development process and ensuring the reliability and performance of your Java applications.

Install Unlogged, record and replay java methods, track code coverage, mock external and downstream calls, and create perfectly working JUnit tests. 

