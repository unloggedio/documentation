# Common Errors  

## Errors with Direct Invoke

--Explain shortly how Direct invoke works--

--List down all the errors related to direct invoke.


## Errors with Logging 

[unlogged-sdk](https://github.com/unloggedio/unlogged-sdk) logs code execution and [unlogged-plugin](https://plugins.jetbrains.com/plugin/18529-unlogged) scans these logs and creates test candidates. 

!!! failure "Failed to serialize response object"
	There are a few fields we can't serialize. You will see the error: 
	```Failed to serialize response object of type``` This means that the object, Pojo or an extended object can not be serialized. 

Here is a list of Pojos/Objects that can't be serialized:





