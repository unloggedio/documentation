# Selective Logging

The SDK can be configured to define the frequency with which methods should be logged. This improves the performance impact of running user application with SDK significantly. The **default behavior** is to log all calls to a method.

## Logging Series
When a frequency counter is defined for a method, then that method would be logged at that frequency. For example if a method is configured to be logged at `counter=2`, then it's 1<sup>st</sup>, 3<sup>rd</sup>, 5<sup>th</sup>, 7<sup>th</sup>, 9<sup>th</sup> ... call will be logged. More strictly, if a `counter "c"` is defined for a method then it's <code>(nc+1)<sup>th</sup> call</code> will be logged where n is a whole number.

!!! Bolt "Live Window"
	Direct invoke of a method will always work with any counter. But the call will show in live window only if that call of method was logged.

## Level of logging configuration
This configuration can be defined at many levels of the code hierarchy. These are:

### 1. Process based logging counter
A blanket counter can be applied to the process, that will apply to all methods until overridden. This can be done as an parameter to the `Unlogged` annotation. The parameter value needs to be a long passed as a string to the processor. An example with counter 10 is defined below.

```java
package org.unlogged.demo.unloggedapplicaton;

import io.unlogged.Unlogged;
import org.springframework.boot.SpringApplication;

public class Application {

	@Unlogged(counter = "10")
	public static void main(String[] args) {
		SpringApplication.run(Application.class, args);
	}
}
```

### 2. Class based logging counter
A counter can be applied to the class, that will apply to all it's methods. This can be done as an parameter to the `UnloggedClass` annotation. The parameter value also needs to be a long passed as a string to the processor. An example with counter 10 is defined below.

```java
package org.unlogged.demo.unloggedapplicaton;

import io.unlogged.UnloggedClass;

@UnloggedClass(counter = "10")
public class temp {

    public long sumRange(long n) {
        long sum = (n*(n+1))/2;
        return sum;
    }
}
```

### 3. Method based logging counter
A counter can be applied to an individual method. This can be done as an parameter to the `UnloggedMethod` annotation. The parameter value needs to be a long passed as a string to the processor. An example with counter 10 is defined below.

```java
package org.unlogged.demo.unloggedapplicaton;

import io.unlogged.UnloggedMethod;

public class temp {

    @UnloggedMethod(counter = "10")
    public long sumRange(long n) {
        long sum = (n*(n+1))/2;
        return sum;
    }
}
```

### Priority order of frequency counters
- A method's logging counter can have conflicting rules. Then they take precedence based on the following order:
```
process level < class level < method level
```
- For example, a application can have `process counter=10`. It can have a class `StudentController` with `class counter=100`, and two methods `getAllStudents` with `method counter=1000` and `getExamData` with no method annotation.
Then `getAllStudents` will have `counter=1000` and it will override the class and process wide counter. The `getExamData` will have the `counter=100`, from class level.

## Special Methods and there logging
Some methods are probed/unprobed based on logic outside of above rules. These rules override any other logic defined at other level.

### 1. Always Probed Method
Some method are always probed. These are:

- methods of an interface
- methods of a enum
- constructor method
- starting method of process (the `public static void main() ` method)

### 2. Never Probed Method
The method with following names are never probed:

- `equals`
- `hashCode`
- `onNext`
- `onSubscribe`
- `onError`
- `currentContext`
- `onComplete`
- Also any abstract method is never probed.

!!! Tip "Deployment Strategy"
	The selective logging is a recommended strategy for deploying your application with SDK in production and pre-production environments. There should be a moderate frequency counter process wide. **Stable classes/methods** that are called many times should have extremely high counter values. **Experimental classes/methods** should have a lower counter value to log a wider range of traffic.
