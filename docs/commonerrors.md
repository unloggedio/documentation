# Common Errors  

## Direct Invoke

```DirectInvoke``` communicates with your application using a custom RPC implementation inside the unlogged-sdk. The RPC is active when there is an ```@Unlogged``` annotation on the class executed.

The RPC includes:

- Class name
- Method name
- Method signature
- Parameter types
- Paramter values
- Mock definitions

The command executor in unlogged-sdk gets an instance of `ClassName`. It gets the instance in one of the two ways

- Last seen instance of type ClassName
- Try to create a new one if no existing instance exists 

!!!	tip 
	In case the command executor tries to create a new instance, it uses the no-arg constructor.


## What can go wrong?

### Object Serialization and Deserialization

Unlogged converts an object to a ```json``` using a serializer and stores it bytestream. Later, we deserialize the object to a json. 


!!! failure "Object serialization/deserialization"
	Unlogged uses jackson for serialization/deserialization. 
	If jackson is unable to serialize any parameter or return value then it shows up as its long id hash code.
	This can affect you while using DirectInvoke or Generate JUnit Test Case.


### java.lang.NullPointerException

You may come across ```NullPointerException``` while using Direct Invoke. Here are possible explainations:

#### Value of a field is null

When ```Direct Invoke``` is used on non-service classes so that no recently used instance is available - Unlogged creates a new instance of this class, using no-arg constructor. This means that a few feilds may be uninitialized. In this case, you will run into a ```Null Pointer Exception```

#### A local variable based on input parameter is null

Make sure the parameter values you are passing are correct and the associated data exists if downstream calls are not mocked.

#### Cannot invoke "java.lang.reflect.Field.getType()" because "field" is null

This means that one of the parameter required to execute the method could not be created. It could be due to different reasons.

#### Authentication is empty

When the method being executed expects an Object in the ```SecurityContextHolder```, it will receive null and throw an NPE if it tries to invoke a method on the expected return object. 

#### No transaction found

When using ```@Transacational``` annotation on methods, currently the code using transactions will fail since no transaction is created when method are executed. 

!!! tip
	Support for ```@Transacational``` annotation, ```SecurityContextHolder``` and parameterized constructors is coming soon. 

