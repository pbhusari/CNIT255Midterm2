# Lecture 18 - Exceptions Part 1



**Q: When an error occurs, what can a program do?**

A: Return to a safe state, save the user's work and terminate

**Q: What types of errors do you need to consider?**

A: User Input errors, device errors and physical limitations, code errors

**Q: What can you do when an error occurs?**

A:
+ Return an error code
+ Terminate the program
+ Throw and exception

**Q: What is an exception?**

An exception is a *type of error* what can be broken up into two categories

*Q: What is an unchecked exception?*

Runtime Exceptions arise from faults of the programmer. They also go by the name of *unchecked* exceptions because the compiler *does not* check for these at compile time.

Another type of *unchecked* exception is an error. 

Typically, you do *not* handle these in a try-catch block on principle of good practice. A good programmer could avoid these exceptions completely.

Examples of unchecked exceptions inlcude:
   + NullpointerExceptions
   + OutOfBounds
   + ... 

*Q: What is a checked exception?*

An unchecked exception could be thought of  as a "fact of life” in the sense that a good programmer could not account for them perfectly. 

This is because rather than arising from the programmer itself, these checked exceptions arise from faults of the environemnt such as

+ Flaky network connections
+ Files that were just moved
+ ...
+
The compiler **checks** that you dealt with them as a programmer at compile time using a try-catch block.

Examples of checked exceptions include:

+ EOFException
+ IOException
+ ...


**Q: How can exceptions be thrown by the programmer?**

The first step is to find what type of exception that you want to throw. In this case, you want to throw an `EOFException` because the user's header and the file length do not match. 

You would construct an exception object and throw it with the following syntax:

```java
throw new EOFException();
```

Or better yet, you can elaborate on the error with a `gripe` string 

```java
String grip = "Content lentgth: " + len + ", Recived: " + n;
throw new EOFException(gripe);
```

**Q: But what if your exception is not included in the standard library?**

You can create your own exception class. The more specific the class your homemade exception extends, the better.

Lets say that we also want to add a case where a user uploads a file of the worng format. We would declare an exception class `FileFormatException` that *extends* the `IOException` class.

```java
class FileFormatException extends IOException{
	public FileformatException() {	// Blank constructor for throws 
        super();					// without gripes
	}
	public FileFormatException(String gripe){ // Constructor for throws
        super(gripe);						  // with gripes
	}
}
```

Then, you can throw this exception in your own code using this syntax

```java
if ( ... ) throw new FileFormatException();
```

**How would you handle these exceptions when they are thwon?**

Instead of terminating the program, you can use a try catch block to *catch* an exception that was *thrown*.

For example, if you regularly want to execute `code()` but if `code()` thwos an exception of `ExceptionType e`, then it moves onto the catch block.

```java
try 
{
	code();
} 
catch (ExceptionType e) 
{ 
//	handler for this type
	handle();
}
```

Note that you can chain these try catch blocks to handle multiple types of exceptions:

```java
try 
{
	code();
} 
catch (FileNotFoundException | UnknownHostException e) 
{ 
	//emergency action for missing files and unknown hosts 
	...
} 
catch (IOException e) 
{ 
	//emergency action for all other I/O problems 
	...
}
```

**Q: What if you want to execute code reguardless of any exception?**


If you want to execute code right after these try catch blocks in every circumstance, such as closing a relinqushed resource, you use a `finally` block. This way, your code is guarunteed to give back your resources, exception or not.

```java
//giving up the resource
PrintWriter out = new PrintWriter(. . .);
try 
{
	//code that might cause an exception
	. . . 
} 
finally 
{ 
	//taking back the resource
	out.close(); 
}
```

**What if you want to see the origin of an exception as a program is running?**

You can *trace back* an exception with the `printStackTrace();` method of the `Exception` class to list pending method calls.  