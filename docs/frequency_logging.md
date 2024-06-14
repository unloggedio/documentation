# Frequency Logging

The SDK can be configured to define the frequency with which methods should be logged. This improves the performance impact of running user application with SDK significantly. The **default behaviour** is to log all calls to the method.

## Logging Series
When a frequency counter is defined for a method, then that method would be logged at that frequency. For example if a method is configured to be logged at `counter=2`, then it's 1<sup>th</sup>, 3<sup>rd</sup>, 5<sup>th</sup>, 7<sup>th</sup>, 9<sup>th</sup> ... calls will be logged. More strictly, if a `counter "c"` is defined for a method then it's <code>(nc+1)<sup>th</sup> call</code> will be logged where n is a whole number.

!!! Bolt "Live Window"
	Direct invoke will always work with any counter of logs. But the call will show in live window only if that call of method was logged.

## Level of logging configuration
This configuration can be defined at many levels of the code hierarchy.

### 1. Process based logging counter
A blanket counter can be applied to the process, that will apply to all methods. This can be done as an parameter to the `Unlogged` annotation. The paramater value needs to be a long passed as a string to the processor. An example with counter 10 is defined below.

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
A counter can be applied to the class, that will apply to all it's methods. This can be done as an parameter to the `UnloggedClass` annotation. The paramater value needs to be a long passed as a string to the processor. An example with counter 10 is defined below.

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
A counter can be applied to an indivisual method. This can be done as an parameter to the `UnloggedMethod` annotation. The paramater value needs to be a long passed as a string to the processor. An example with counter 10 is defined below.

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
- If method's logging counter have conflicting rules, then they take precendence based on the following order:
```
process level > class level > method level
```
- For example, a process can have `counter=10`. It can have a class `StudentController` with `class counter=100`, and two methods `getAllStudents` with `method counter=1000` and `getExamData` with no method annotation.
Then `getAllStudents` will have `counter=1000` and it will overwrite the class and process wide counter. The `getExamData` will have the `counter=100`, from class annotation.

## Special Methods and there logging
Some methods are probed/unprobed based on logic outside of the gambit of above logic.

### 1. Always Probed Method
Some method are always probed. These are:

- methods of an interface
- methods of a enum
- methods of a static class
- static method
- constructor method
- starting method of process

### 2. Never Probed Method
Some methods are never probed, these have the following names:

- `equals`
- `hashCode`
- `onNext`
- `onSubscribe`
- `onError`
- `currentContext`
- `onComplete`.

!!! Tip "Deployment Strategy"
	The frequency logging is a recommended starategy for deploying your application with SDK in production and pre-production environments. There should be a moderate frequency counter process wide. **Stable classes/methods** and called widely should have extremly high counter values. **Experimental classes/methods** should have a lower counter value to log a wider range of traffic.
