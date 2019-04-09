# Lecture 19 - Exceptions Part 2

**Are errors always thrown in the same way all the time?**

Of course not, programmers are a varied bunch and libraries are used for multiple different purposes. For example, if you wanted to take the square root of a negative number with `Math.sqrt(x);`, it would return `NaN` instead of a `mathError`. 

This is not a fault of the library itself, but it can produce problems down the line, such as vague `nullPointerExceptions` if you try to cast `NaN` as a long decimal from its original double form.

**Why not just use if statments and throws?**

The reason why a programmer would use asserts instead of an if statment like the one below is that if statments are terrible for efficiency's sake, especially if its for testing. 

```java
if (x < 0) throw new IllegalArgumentException(“x < 0”);
```

Such structures are hard to evict from production code whereas assertions can be toggled by addint the  `-disableAssertions` at the end of a `javac` (compile) or `java` (execute) command.

**How would you provide an error checking solution that is both comprehensive AND efficient?**

Assertions are a toglable way to throw errors when testing code. Unlike if statments, they can be disabled on compilation or runtime.  The syntax for asserting a `double` variable  `x` is as follows:

```java
assert x>=0;
```

To further aid in bug squashing, the programmer can pass a message, or a stringified version of an object through an assert statment as follows.

```java
assert x>=0 : x
```

**How do you enable assertions?**

By default, assertions are enabled. To enable them manually, run your java program (in this case `MyApp`) with the `-enableAssertions` flag.

Conversly, use the `-disableAssertions` flag to disable assertions on runtime.

**But what if I want to enable/disable assertions on a class by class basis?**

To do so, use this syntax

```
java –ea:MyClass –ea:com.horstmann.corejava –da:AnotherClass MyApp
```

**When exactly would you use assertions?**

When you want to *terminate* a program on a non-vauge basis (no nullPointerExceptions).

Typically when testing assumptions, such as in the case below

 ```java
if(i % 3 == 0)
{
	...
}
else if (i % 3 == 1) 
{
	. . .
}
else {
	assert i % 3 == 2; //Assuming all else statments flow here
	. . .
}
 ```

Or better yet, you can also state the assumption that i is a positive integer by *asserting* that i *is greater than or equal to* 0

```java
assert i>= 0
```

**Q: Why use logging instead of ** `System.out.println()` **calls ?**

1. You can supress reports given a log level to filter for specific results
2. Log records are directed to different handlers (i.e. not populating the console with garbage)
3. Logging configuration is controlable by a config file, making it independent of your code

**Q: How would you log an aciton such as opening a menu item?**

You would use the following syntax in your implementation

```java
Logger.getGlobal().info('File->Open menu item selected');
```

**Q: What do these logs look like?**

The include a dateTimeStamp, the class name, the method, and the message specified by the programmer.

```
May 10, 2013 10:12:15 PM LoggingImageViewer fileOpen INFO: File->Open menu item selecte
```

**Q: How would you supress logger messaages?**

You would set the global logger level to off by using the following syntax:

```java
Logger.getGlobal().setLevel(Level.OFF);
```

 Done.
