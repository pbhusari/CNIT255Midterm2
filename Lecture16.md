# Lecture 16 - Interfaces

**Q: What is an interface?**

A: An interface is a *set of requirements for a class*. However, unlike abstract classes, a class can conform to one or many interfaces.


**Q: Are interfaces classes?**

A: No, they are not classes. The best way to think of a class is as a person, place or thing. An interface is none of those, instead, think of them as a *service provider*


Say that you want to be able to sort all classes that `implement` the `compareTo` interface. First, you would need to define the interface `compareTo`.

```java
 public interface Comparable { 
     int compareTo(Object other); //automatically public 
 }
```

Then, in your following class that `implements` the interface `Comparable`, you would modify the class header and override the `compareTo` service that the interface provided

```java
public class Employee implements Comparable 
{ 
	public int compareTo(Object otherObject) 
	{
    	Employee other = (Employee) otherObject; 
    	return Double.compare(salary, other.salary); 
    } 
	. . .
}
```

In this case, we made employees `compareTo` themselves reguarding the salary.

*Python data model note: Think of this as operator overloading, all classes can respond to certain "operators" to make the classes more user friendly. Also notice that this ** implementation** uses `Double` (wrapper class)'s `compareTo` method*

Note: you can do away with casting and use generics, this way the syntax is way friendlier and readable

```java
class Employee implements Comparable<Employee> 
{ 
	public int compareTo(Employee other) 
	{ 
	return Double.compare(salary, other.salary); 
	} 
	. . . 
}
```

*Python data model note: just like how itemOf can lead to implementations with random.shuffle() and itertools.enumerate(), so too can comparibles lead to implementations of sorting algorithims*

```java
if (a[i].compareTo(a[j]) > 0) 
{ 
	// rearrange a[i] and a[j] 
	. . . 
}
```

Here, the interface `compareTo`'s implemetnation in object `a[i]`'s class is used in a sorting algorithim.

**Q: how does the compiler know that ** `a[i].compareTo(a[j])`**is valid? **

A: The compiler does not know, you declare the method itself to act on `comparable` objects in the following line:

```java
public static void sort(Comparable[] a)
```

**Q: Can you instantiate an interface?**

A: No, you cannot ,because *interfaces are not classes*

**Q: can you have variables of interface type?**

A: Yes, provided that the variable points to an object of a class that represents the implementation, as shown below,

```java
Comparable x;
x= = new Employee(...) //OK as long as employee implements comparable
```

**Q: How do you know if an object `implements` an interface in code?**

A: You use an `instanceOf` check

```java
if (anObject instanceof Comparable)
{
    ...
}
```

This is useful when you do not want to make a try catch block and run into vague errors such as ``nullPointerException``s

**Q: Can interfaces be extended?**

A: Yes, as shown in the example below.

```java
public interface Moveable
{
    void move(double x, double y);
}

public interface Powered extends Moveable
{
    double milesPerGallon();
}
```

This is useful in cases where you want to organise interfaces *as a type* of one another. In this case, a powered block is both moveable (has to implement `move()` method) and has a `milesPerGallon` method requirement.

**Q: Can a class implement multiple interfaces?**

A: yes, just add commas between them. No need for another `implements` keyword.

```java
public class Employee implements Comparable,Moveable 
{
	...    
} 
```

**Q: What are the properties of fields in interfaces?**

A: They are always 

+ Public
	* Accsessible by the world 	
+ Static
	* Not with by any object
+ Final 
	* Cannot be changed
	* Goes along with the `public` keyword 

*Style note: interfaces Are Always Capitalized  as To Not Be Confused With Methods or Instance Vars*

**Q: Why not just use abstract classes and inherrit from those instead of using interfaces?**

A: Because java does not have *multiple inherritance* meaning that a class cannot extend two or more classes at a time, as illustrated below

![abstractNotInterface](C:\Users\prana\Desktop\CNIT 255 Midterm 2\img\abstractNotInterface.PNG)



This becomes problematic when you want to implement two or more interfaces at the same time, say in a deck of cards that needs to be both *sliceable* and *comparable* in the case of a game of war. You simply have to use interfaces in a case like this



```java
public class Cards implements Compareable<Cards>, SliceAble
{
	...
	public int CompareTo (Cards other)
    {
    	return Double.comapre(sum, other.sum)
    }
    public Cards Slice (beginingIndex, endingIndex)
    {
    	return deck.sublist(beginingIndex, endingIndex)
    }
}
```

And that is that.
