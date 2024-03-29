# The Four Pillars of Object-Oriented Programming

JavaScript is a multi-paradigm language and can be written following different
programming paradigms. A programming paradigm is essentially a bunch of rules
that you follow when writing code, to help you solve a particular problem.

That's what the four pillars are. They're software design principles to help
you write clean Object-Orientated code.

The four pillars of object-oriented programming are:

- Abstraction
- Encapsulation
- Inheritance
- Polymorphism


## Abstraction

Abstraction is a way to reduce complexity and allow efficient design and
implementation in complex software systems. It hides the technical complexity
of systems behind simpler APIs.

JavaScript abstraction refers to the concept of hiding complex implementation
details and showing only the essential features or functionalities of an object
or module to the user

Creating abstraction in JavaScript involves organizing your code in a way that
hides complex details and exposes only the essential features to other parts of
your program. 

Advantages of Data Abstraction:
- Helps the user to avoid writing low-level code.
- Avoids code duplication and increases reusability.
- Can change the internal implementation of a class independently without  
  affecting the user.
- Helps to increase the security of an application or program as only  
  important details are provided to the user.


## Encapsulation

Objects provide an interface to other code that wants to use them but maintain
their own internal state. The object's internal state is kept *private*, meaning
that it can only be accessed by the object's own methods, not from other objects.
Keeping an object's internal state private, and generally making a clear division
between its public interface and its private internal state, is called **encapsulation**.

Removing access to parts of your code and making things private is exactly what
Encapsulation is all about.

Private properties are achieved in JavaScript by using closures.


## Inheritance

Inheritance lets one object acquire the properties and methods of another object.
In JavaScript this is done by **Prototypal Inheritance**.

Whenever we use inheritance, we try to make it so that the parent and the child
have **high cohesion. Cohesion** is how related your code is.

When using inheritance, you should require most of the functionality (you don't
always need absolutely everything).

## Polymorphism

Polymorphism means "the condition of occurring in several different forms."


---

### Resources

- https://dev.to/kevin_odongo35/object-oriented-programming-with-typescript-574o
- https://dev.to/cliff123tech/oop-typescript-jk4
