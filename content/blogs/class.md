---
title: "Les classes en C#"
date: 2023-10-14T16:42:00
draft: false
author: julioz, kolowy
toc: false
tags:
    - C#
---

What is a class?
A class is like an <code>object</code>. In this example, we will consider a class <code>Person</code>.
We can add <code>attributes</code> to the class. Attributes are sort of variables that are defined in the class and belong to the object they are defined in. For example, for a class <code>Person</code>, we can create the attributes <i>name</i> and <i>age</i>, that  will contain the person's information.

Let's create a house class as an example:

```cs
class Person
{
    private string name; // a attribute, for the person's name
    private int age; // another attribute, for the person's age
}
```

We might want to access to those attributes, using the keyword <code>public</code>. A <code>getter</code> is a way to look at the value of the private variable from outside its  class. A <code>setter</code> is like a way to change the value of the private variable from  outside the class. They are called <code>properties</code> of your attributes. You can create them this way:
```cs
class Person
{
    private string _name;
    private int _age;

    public string Name // property for the name
    {
        get { return _name; } // getter
        set { _name = value; } // setter
    }

    public int Age // property for the age
    {
        get { return _age; } // getter
        set { _age = value; } // and a setter
    }
}
```

You can also do it in a shorter and easier way:

```cs
class Person
{
    public string Name { get; set; } // getter and setter for the attribute Name
    public int Age { get; set; } // getter and setter for the attribute Age
}
```

Now, we want to do some stuff with our class, and to do so, we will use <code>methods</code>. They defind the actions the class can do.

```cs
class Person
{
    public string Name { get; set; }
    public int Age { get; set; }

    public void HeyYou() // a method
    {
        Console.WriteLine($"Hey, I am {Name}, I'm {Age} years old!");
    }

    public void CheckTime(string time) // another method
    {
    Console.WriteLine($"What time is it, {Name}?");
    if (time == "Friday")
        Console.WriteLine("Check my time, it's Friday");
    else
        Console.WriteLine("I don't know");
    }
}
```
 A <code>constructor</code> is a method that is called when you create a new object of your  class. It is used to set the initial state of the object.
 This method is a bit special, because it has no return type and <b>MUST</b> have the exact same name as the class. It's even more special because it won't be called like other methods, but we'll see that a bit later.

```cs
class Person
{
    public string Name { get; set; }
    public int Age { get; set; }

    public Person(string name, int age) //the constructor
    {
        this.Name = name;
        this.Age = age;
    }

    public void HeyYou()
    {
        Console.WriteLine($"Hey, I am {Name}, I'm {Age} years old!");
    }

    public void CheckTime(string time)
    {
        Console.WriteLine($"What time is it, {Name}?");
        if (time == "Friday")
            Console.WriteLine("$Check my time, it's Friday");
        else
            Console.WriteLine("I don't know");
    }
}
```

Now, you can create your first Person, called an <i>instance</i>. An instance is a specific object created from the class. Here, your instance is stored in the variable <code>smurf</code>. Each instance has its own attributes name and age, and holds the methods of the class <code>Person</code>:

```cs
Person smurf = new Person("Smurf", 20);
Person smourf = new Person("Smourf", 15);
smurf.HeyYou();             // Hello, I'm Smurf, I'm 20 years old!
smourf.HeyYou();            // Hello, I'm Smourf, I'm 15 years old!

smourf.Name = "Smorf";
smurf.Age = 21;
smurf.HeyYou();             // Hello, I'm Smurf, I'm 21 years old!
smourf.HeyYou();            // Hello, I'm Smorf, I'm 15 years old!

smurf.CheckTime("Friday");  // What time is it, Smurf ?
                            // Check my time, it's Friday
```

<h2>Public or private?</h2>
We have seen what a public set is. Now, we will introduce a new keyword: <code>private</code>.
First of all, let's talk about the difference between a <code>public</code> member and a <code>private</code> one.
The <code>public</code> members are accessible from both inside and outside of the class they are defined in.
The <code>private</code> members are only accessible from within the class they are defined in. It is the default access of a member.
It is the same thing for <code>sets</code>. In comparaison to a <code>public set</code>, a <code>private set</code> adds restriction to the modification of the property. Indeed, the <code>private</code> keyword will block all the extern modification, therefore you can only modify the property in a method of the same class. This way, other external classes cannot directly modify its value.

```cs
class Person
{
    public string Name { get; private set; } // getter and private setter for the attribute Name
    public int Age { get; set; } // getter and setter for the attribute Age
}

class Program
{
    public static void Main()
    {
        Person person = new Person();
        person.Name = "Test."; // This line will produce an error. In the class Program, we can't modify the Name of the instance
        person.Age = 12; // But we could modify the Age of the instance
    }
}
```
