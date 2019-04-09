# Lecture 17 - Inner Classes

==**Q: What is an inner class?**==

A: A class that is defined inside of another class

 ==**Q: Why use an inner class in the first place?**==  

A: Use an inner class to hide implementation details. Typically you only use inner classes when one class is only relevant to another on in terms of functionality.
This further increases encapsulation, and makes packages neater.

## Example 1:

```java
public class TalkingClock 
{
	private int interval; 
	private boolean beep; 
	
	public TalkingClock(int interval, boolean beep) //outer class method
	{ 
		. . . 
	} 
	public void start()  //outer class method
	{ 
		. . . 
	}
	
    public class TimePrinter implements ActionListener 
    { 
    	public TalkingClock bird;
    	
        public void actionPerformed(ActionEvent event) 
        { 							
            System.out.println(“At the tone, the time is ” + new Date()); 
            if (beep) Toolkit.getDefaultToolkit().beep(); 
        } 
    }
}
```

**Note that this relationship IS NOT **


1. **Association**
2. **Inheritance**
3. **Composition**

In this class `TalkingClock` DOES NOT have a `TimePrinter` inside.

==**Q:  Based on the code above, where does **== `beep()` ==**come from?**==

A: In this case, beep comes from its *outer class* field, talking clock. For all inner classes, the inner class object has a reference to the outer class object that created it.

To accsess the outer class from an inner class method, you can use `talkingclock.this.beep`. 

**Q: But what if you wanted to accsess the variables of an inner class from outside of the outer class?**

A: In this case, we want to accsess the `talkingClock` object `bird`. The syntax to accsess  this is `talkingclock.timeprinter.bird` . 

==**Q: How would you construct an inner class object?**== 

A: You can use the following syntax: `OuterClass.InnerClass()`. Say that we wanted to create a new `TimePrinter` object globally name listener. We would use  the following code:

```java
TalkingClock jaberer = ...;
TalkingClock.TimePrinter listener = jaberer.new TimePrinter();
```

==**Q: What is a local inner class?**== 

A: A local inner class is a *class defined inside a method*. In this case, these local classes are only accessible from *inside* of the method, further increasing encapsulation.

```java
public void start() 
{ 
	class TimePrinter implements ActionListener 
	{ 
		public void actionPerformed(ActionEvent event) 
		{ 
			System.out.println(“At the tone, the time is ” + new Date()); 
			if (beep) Toolkit.getDefaultToolkit().beep(); 
		} 
	} 
	ActionListener listener = new TimePrinter(); 
	Timer t = new Timer(interval, listener); 
	t.start(); 
}
```
