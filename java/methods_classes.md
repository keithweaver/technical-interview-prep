# What is a static method?

A method that does not need to be instantiate and can "stand" on it's own.

# When do you use a static method?

- Don't need to instantiate it
- Often utility methods
- Android:

# What is an inner class?

It is a method written inside another class.


# Static Inner vs Non Static Inner Class

An inner class cannot be static.

# Static and non static nested class

A non-static nested class has full access to the members of the class within which it is nested.

A static nested class does not have a reference to a nesting instance, so a static nested class cannot invoke non-static methods or access non-static fields of an instance of the class within which it is nested.


# What is Inheritance?

A Java interface is a bit like a class, except a Java interface can only contain method signatures and fields.

An Java interface cannot contain an implementation of the methods, only the signature (name, parameters and exceptions) of the method.


A class that implements an interface must implement all the methods declared in the interface.


```
public interface MyInterface {
    public String hello = "Hello";
    public void sayHello();
}
```

Then accessing it with:

```
public class MyInterfaceImpl implements MyInterface {
    public void sayHello() {
        System.out.println(MyInterface.hello);
    }
}
```

# What is an Abstract class?

Abstract classes cannot be instantiated, but they can be subclassed. If a class includes abstract methods, then the class itself must be declared abstract, as in:

# When to Use Abstract Class

Abstract class is used when you have scenario that all classes has same structure but some same and some different functionality.


You want to share code among several closely related classes. You want to declare non-static or non-final fields. This enables you to define methods that can access and modify the state of the object to which they belong.

# When to Use Interface

Interface is used when you have scenario that all classes has same structure but totally have different functionality.

You expect that unrelated classes would implement your interface. You want to specify the behavior of a particular data type, but not concerned about who implements its behavior.

# How to extend?

```
public class Child extends Parent {

}

public class Parent {

}
```

# Can a child access a parent methods, constructor, or variables? What types?

Yes to methods assuming not private. Yes with constructor using super. Yes to variables if not private.

# Can a parent access a child's methods, constructor, or variables? What types?

No

# Can an abstract method be private?

# Benefits to using an abstract class?

# Describe a situation when you would use an abstract class.

# When is an abstract class not the best choice?

Source:
- https://stackoverflow.com/questions/10040069/abstract-class-vs-interface-in-java
- https://stackoverflow.com/questions/1353309/java-static-vs-inner-class
- https://stackoverflow.com/questions/2671496/java-when-to-use-static-methods
- https://stackoverflow.com/questions/2773824/difference-between-hashset-and-hashmap
- https://docs.oracle.com/javase/tutorial/java/IandI/abstract.html
