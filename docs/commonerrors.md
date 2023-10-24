# Common Errors  

## Errors with Direct Invoke


DirectInvoke communicates with your application using a custom RPC implementation inside the unlogged-sdk. The RPC is active when there is a @Unlogged annotation on the class executed.

The RPC includes these details:

- Class name
- Method name
- Method signature
- Parameter types
- Paramter values
- Mock definitions

The command executor in unlogged-sdk gets an instance of `ClassName`. It gets the instance in one of the two ways

1. Last seen instance of type ClassName
2. Try to create a new one if no existing instance exists (using the no-args constructor)


## Errors with in DirectInvoke

### Object Serialization and Deserialization

!!! failure "Object serialization/deserialization"
	If jackson is unable to serialize any parameter or return value then it shows up as its long id hash code.
	This can affect you while using DirectInvoke or Generate JUnit Test Case.


### java.lang.NullPointerException

1. Value of a field is null

Frequently in scenarios where DirectInvoke is used on non-service classes such that no recently used instance is available, the instance created using the default no-args constructor will leave the fields uninitialized. Support for args based constructor is coming soon.

2. A local variable based on input parameter is null

Make sure the parameter values you are passing are correct and the associated data exists if downstream calls are not mocked.



### Cannot invoke "java.lang.reflect.Field.getType()" because "field" is null

This means that one of the parameter required to execute the method could not be created. It could be due to different reasons.

### Authentication is empty

When the method being executed expects an Object in the SecurityContextHolder, it will receive null and throw an NPE if it tries to invoke a method on the expected return object. Support for this will come in future version.

### No transaction found

When using @Transacational annotation on methods, currently the code using transactions will fail since no transaction is created when method are executed. Support for this will come in future version.

