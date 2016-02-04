# Scala interview questions over the phone

## Intro

This is a compilation of questions in interviews for scala roles and the best answers having the constraints of a telephonic interview.

## Questions
### What is a case class?

I like to say that a case class is a class with super powers. 
It has a concise syntax to define a class with some inmutable public attributes and it provides implementations for pretty print, apply and unapply among other super powers.

Why is that interesting? Having the apply and unapply methods implemented for you, you can use pattern matching over your class, one of the most powerful techniques in functional programming. 

### How can you get the value of a Future?

If you have a Future holding some future value, you can access it and use it or transform it using map or flatmap, this will return another Future holding some future value related to the first one. 

In your test, or in exceptional cases in your production code, you can block the execution until the future value is calculated using Await. Of course, this must be done with caution.

### If you use futures inside a for comprehension, they are executed sequentially, what can you do so they are executed in parallel?

Without entering in details, basically a Future in scala, starts its computation when it is created. 

If you have a for comprehension that execute two independent calculations sequentially and wait for both to finish, and you want the two calculations to be executed in parallel, then you should create the Futures before the for comprehension.

### Can you explain the supervision strategy in Akka actors?

The supervision strategy is a powerful tool in Akka actors to create resilience applications, following the principle "Let it crash".

The actors are organized as a tree, there is a root actor that is the ancestor of all the actors in an application. Every actor supervise its children and can apply different strategies to handle errors occurred in them. Typical strategies are restart the failing child, or restart all the children, or ignore the problem. 

This way every actor is relieved of the responsibility of handling unexpected errors. The parent is in a better position to assess what is the best strategy and in case it is not prepared for that, the error will propagate up until the error is handled. 

### What is the meaning of the keyword sealed in scala? 

Scala as an object oriented functional programming language allows inheritance. The keyword sealed means that inheritance of this class or trait is only allowed withing the same file. 

Why is that interesting? Because when you are doing a matching over the super class you can patter match any of the subclasses and obtain all the data you need in your function, and if the pattern matching implemented does not cover all the possibilities the compiler will be able to tell you that.

When you are designing you algebraic data type, or just your hierarchy of classes using a sealed trait or class can give you better static analysis on your code, reducing the possibility of bugs.




