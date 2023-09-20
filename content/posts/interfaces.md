+++
title = 'Interfaces in C#'
date = 2023-09-20T02:20:06+01:00
draft = false
categories = ["CSharp"]
showReadingTime = true
ShowShareButtons = true
+++

## What are Interfaces in C# ?

Interface is similar to a class, but only specifies the behaviour of what it does instead of storing data.\
So let us explore what an interface is with an analogy. So let's imagine we have a restaurant menu as an interface. The menu lists a variety of dishes the customer can order.The kitchen team knows how to prepare each dish in the menu's description as per the interface contract. Regardless of the chef's specialization as long as they follow the menu's instructions, customers will recieve what they ordered.
_The menu can be treated as an interface between the customer and chef's._

Now let's visualise this in code let's create a interface for the restuarant menu

```
    // defining an interface
    interface IRestaurantMenu
    {
        void PrepareStarters();
        void PrepareMainCourse();
        void PrepareDessert();
    }

```

This is an interface declaration as you can see it is a bit similar to how we define classes. A few things to note here are

1. As a convention an interface name always starts with "I" for ex: IRestaurantMenu,ITeacher etc.
2. Interfaces can only have methods and properties. It cannot contain fields. It is strictly concerned with what can be done with a certain object. for example a teacher, what can a teacher do give lecture, give homework these are some of the things that will come up in the interface not the name of the teacher which is a field.
3. Also you might have noticed that we are just defining the methods there and there is no actual implementation provided. That is becuase an interface is a standard way of doing things and you can have different implementations defined by the implementing classes. For example a Chineese Restaurant would have different dishes from an Italian Restaurant the interface just act as standard in which they all do the same thing which make starters,make mains,make dessert but the implementation of each class is different.

So now let's see what that code above is saying it says that we have declared an interface called IRestaurantMenu. And it also says that a class which implements this interface **MUST** do this three things prepare starters, prepare mains and prepare desserts,It can have as many methods as it wants but those three are necessary that is the main takeaway here. Now let's create a class and see how we can implement this.

```
    public class ItalianRestaurant: IRestaurantMenu
    {
         public void PrepareAppetizer()
         {
        // Implement the preparation of an Italian appetizer
         }

        public void PrepareMainCourse()
         {
        // Implement the preparation of an Italian main course
         }

        public void PrepareDessert()
         {
        // Implement the preparation of an Italian dessert
         }

         public void PreparePizza()
         {
        // Implementat the preparation of pizza
         }

    }


```

Here we have a class implementing the interface the syntax is similar to a class child class inheriting from the parent class. But the thing with interfaces is that a class can implement more than one interface for exmple let's say we have a resturant that implements both the CustomerService interface and the RestaurantMenu interface.

```
    public class Restaurant: ICustomerService,IRestaurantMenu
    {
        // implement the class functionality
    }

```

I have added a method called PreparePizza from which you can see that you add more methods if you want but those three represent the core of what a restaurant should do.

### So why do we need interfaces ?

Perhaps the most important use of interfaces is in a concept of [**Coupling**](<https://en.wikipedia.org/wiki/Coupling_(computer_programming)>).Coupling means the interdependance of other software modules.This is often referred to as tight coupling. There are many advantages of decoupled code and it is an important part of computer science because decoupled code can be reused and is an important concept of abstraction.

Let's write an example and see what I mean by coupling

```
    class PaymentProcessor
    {
        public void ProcessCreditCardPayment(CreditCard creditCard, decimal amount)
        {
            // Code to process credit card payment
        }

        public void ProcessPayPalPayment(PayPalAccount payPalAccount, decimal amount)
        {
            // Code to process PayPal payment
        }
    }

```

Here , You can see that the ProcessCreditCardPayment and ProcessPayPalAccount are dependant on the input they recieve CreditCard and PayPalAccount respectively. So, in any changes happen to those classes you will have to change the implementations inside the PaymentProcessor class.This is what is called tight coupling.

So, let's see how interfaces fix this problem:

```
    interface IPaymentMethod
    {
        void ProcessPayment(decimal amount);
    }

    class CreditCard : IPaymentMethod
    {
        public void ProcessPayment(decimal amount)
        {
            // Code to process credit card payment
        }
    }

    class PayPalAccount : IPaymentMethod
    {
        public void ProcessPayment(decimal amount)
        {
            // Code to process PayPal payment
        }
    }

    class PaymentProcessor
    {
        public void ProcessPayment(IPaymentMethod paymentMethod, decimal amount)
        {
            paymentMethod.ProcessPayment(amount);
        }
    }

```

Let us take a look what is happening here, first we define the interface and then two classes CreditCard and PayPal which implement the interface.Then we create a class PaymentProcessor which implements the payment method you are paying. You can see in the constructor that it is recieving the type of payment `public void ProcessPayment(IPaymentMethod paymentMethod, decimal amount)` as an interface which solves the rigidity we had earlier.Because if you imagine if we now want to introduce another payment method for example ApplePay you can just create a new class which implements the interface and you are good to go you didn't have to touch the other classes or the PaymentProcessor class.This is the power of abstraction that interfaces give us.

### ReImplementing an Interface in a Subclass

A subclass can reimplement any interface member already implemented by a base class.
The member does need to have a virtual in the base class also it doesn't matter whether the memeber is implemented implicitly or explicitly.This just means that if you have a base class that implements an interface and you create a subclass of the base class, the subclass can have it's own implementation for the interface member that base class has already implemented.

let's see an example of this one

```
    using System;

    // Define an interface
    public interface IExample
    {
        void DoSomething();
    }

    // Base class implementing the interface
    public class BaseClass : IExample
    {
        // explicit implementation of Interface member
        public void IExample.DoSomething()
        {
            Console.WriteLine("BaseClass is doing something.");
        }
    }

    // Subclass of BaseClass
    public class SubClass : BaseClass, IExample
    {
        public new void DoSomething()
        {
            Console.WriteLine("SubClass is doing something.");
        }
    }

    class Program
    {
        static void Main()
        {
            IExample example = new SubClass();

            // Calling DoSomething through the interface
            example.DoSomething(); // Output: "SubClass is doing something."
        }
    }

```

In this example, we have an interface `IExample`, a base class `BaseClass` that implements the interface, and a subclass `SubClass` that also implements the interface. Both `BaseClass` and `SubClass` provide their own implementations of the `DoSomething` method.

So when we create a new instance of the SubClass and call the DoSomething method it will print the output to be "SubClass is doing something".

### Catches with interface Reimplementation

Interface reimplementations has a few drawbacks one of them being the sub class has no way of calling the base class method(because the subclass will have it's own implementation of that method). Another one being the author of the base class might not anticipate that a method would be reimplemented in the child class and might not have made necessary changes to keep the code from not breaking.

So,there are few alternatives to interface reimplementation

1. When implicitly implementing a member you have to add the virtual keyword so other people messing around with the code knows that this method can be overridden.
2. When explicitly implementing a member, use the following pattern if you feel that the subclass is going to override it.

```
    public class TextBox : IDrawShape
    {
    void IUndoable.IDrawShape() => DrawShape();    // Calls method below
    protected virtual void DrawShape() => Console.WriteLine ("drawing square");
    }

    public class Rectangle : Square
    {
    protected override void DrawShape() => Console.WriteLine("drawing rectangle");
    }

```

### Default Interface Members

From C# 8 onwards there is an option to provide a default implementation for the interface members

```
    interface ITest
    {
        // implementing the method in the interface
        void PrintSomething(string text) => Console.WriteLine(text);
    }

    public class Testing:ITest
    {
        //creating an empty class that implements the interface

    }


    static void Main()
        {
            // you can see it is of the type ITest not the class Testing
            ITest test = new Testing();

            test.PrintSomething("hello");

        }

```

This is definetely useful when you have to add a new member and not break the implementation of other classes.
Default implementation are always explicit,so in our example earlier the `Testing` class did not implement the `PrintSomething` method which is why a instance won't have access to that method because it is an explicit implementation. So, if we need to use the `PrintSomething` method we need to cast it or initialise it as an `ITest` in our case.
