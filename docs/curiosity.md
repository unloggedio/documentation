# How does this all work?  

[unlogged-sdk](https://github.com/unloggedio/unlogged-sdk) logs code execution and [unlogged-plugin](https://plugins.jetbrains.com/plugin/18529-unlogged) scans these logs and creates test candidates. 

## Unlogged SDK

[unlogged-sdk](https://github.com/unloggedio/unlogged-sdk) adds logging probes to the ```java``` code in compile time.

We have extended lombok's implementation to add such probes automatically. 

Check our [blog post](https://www.unlogged.io/post/how-does-the-lombok-magic-work-underneath) that explains how lombok works 

## Unlogged Plugin

### Direct Invoke

### Scanning Logs

### Extracting Candidates

## Mocking