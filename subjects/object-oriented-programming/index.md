---
layout: default
title: Object Oriented Programming
meta: 
todo: 
---
{% include licence.md %}

## Object-oriented programming

Before we begin, here is a small introduction to object-oriented programming.

In procedural programming - which is the way of programming we have been studying so far - a program is divided in to smaller parts, methods. A method works as a separate part of a program and it can be called from anywhere in the program. When a method is called, execution of the program moves to the beginning of the called method. After the execution of the method is done, the program will continue from where the method was called.

In object oriented programming, just like in procedural programming, we attempt to divide a program into smaller parts. In object-oriented programming the small parts are objects. Each separate object has its own individual responsibility; an object contains a related group of information and functionality. Object-oriented programs consist of multiple objects which together define how the program works.

### Object

We have already used many of the ready-made objects in Java. For example, ArrayLists are objects. Each separate list consists of information related to it; that is, the state of the object. Functionality is also contained in the ArrayList objects: the methods by which the state of the object can be altered. As an example, there are two ArrayList objects in the following piece of code, cities and countries :

```java
public static void main(String[] args) {
    ArrayList<String> cities = new ArrayList<String>();
    ArrayList<String> countries = new ArrayList<String>();

    countries.add("Finland");
    countries.add("Germany");
    countries.add("Netherlands");

    cities.add("Berliini");
    cities.add("Nijmegen");
    cities.add("Turku");
    cities.add("Helsinki");

    System.out.println("number of countries " + countries.size() );
    System.out.println("number of cities " + cities.size() );
}
```

Both the `countries` object and the `cities` object live a life of their own. The state of each is not related to the state of the other. For example, the state of the `countries` object consists of the Strings "Finland", "Germany" and "Netherlands" that are in the list, probably also the information of how many countries are in the list.

When doing a method call related to an object (for example, `countries.add("Finland");`), the name of the object whose method is being called goes to the left side of the period sign (dot), and to the right side goes the name of the method itself. When asking how many Strings the `countries` list contains, we call `countries.size()`. We are calling the method size of the object countries. What the method returns depends on the state of the object in question, other objects do not affect the execution of the method in any way.

We have used the command `new` many times already. For example, creation of a list (`ArrayList`) and creation of a reader (`Scanner`) have been done using the command `new`. The reason is that both of these are *classes* from which the object is created. In Java, objects are always created with `new`, except in a few cases.

One of the cases where you do not always need to use `new` is in the construction of Strings. The familiar way to create a String is actually an abbreviated way of using `new`. A String can also be created with new just like any other object:

```java
String text = "some text";       // abbreviated way of creating a String
String anotherText = new String("more text");
```

Cases in which ready-made parts of Java call `new` out of sight of the programmer also exist.

### Class

It is clear that all objects are not similar to one another. For example, `ArrayList` objects differ drastically from `String` objects. All `ArrayLists` have the same methods `add`, `contains`, `remove`, `size`, ... and respectively all String objects have the same methods (`substring`, `length`, `charAt`, ...). `Arraylist` and `String` objects do not have the same methods because they are different types of objects.

The type of a certain group of objects is called a **class**. `ArrayList` is a class, as are `String`, `Scanner`, and so forth. Objects, on the other hand, are *instances* of classes.

Objects of the same class all have the same methods and a similar state. For example, the state of an `ArrayList` object consists of elements inserted to the list while the state of a `String` object consists of a string of characters.

### A class and its objects

A **class defines** what kind of objects it has:

- **what methods the objects have**
- **what the state of the objects are, or in other words, what kind of attributes the objects have**

A class describes the "blueprint" of the objects that are made out of it (are instances of it).

Lets take an analogy from the world outside of computers: the blueprints of a house. The blueprints define how the building is to be built and in that way dictate the shape and size of it. The blueprints are the class, they define the general characteristics of the objects created out of that class:

![blueprint](images/21_blueprint.jpg)

Individual objects, the houses in our analogy, are made from that same blueprint. They are instances of the same class. The state of individual objects, the attributes, can vary (color of walls, building material of the roof, doors, windowsills, etc...). Here is one instance of a House object:

![house](images/21_house.jpg?thumbmedium)

An object is always created from its class by calling the method - the constructor - that creates the object with the command `new`. For example, a new instance is created from the class Scanner by calling `new Scanner(..)`:

```java
Scanner reader = new Scanner(System.in);
Constructors take parameters the way any other method does.
```

{% include_relative exercises/001.md %}
{: .exercises }

### Defining your own class - object variables

A class is defined to serve some meaningful whole. Often a "meaningful whole" represents something from the real world. If a computer program needs to handle personal data it could be sensible to define a separate class Person which then holds methods and attributes related to an individual.

Let us go ahead and assume that we have a project frame with an empty main program:

```java
public class Main {

    public static void main(String[] args) {
    }

}
```

We will create a new class in our project. In IntelliJ, this can be done in projects on the left, from the right click menu select *new*, *java class*. We will name the class in the dialog that pops up.

Just as with variables and methods, the name of the class should always be as descriptive as possible. Sometimes as a project progresses a class might transform into something different in order meet the programmer's needs. In situations like this, it is possible to rename your class with ease.

Let us create a class named `Person`. The class will exist in its own `Person.java` file. Since the main program is in its own file the program now consists of two files in total. At first the class will be empty:

```java
public class Person {

}
```

The class has to define what methods and attributes the objects created from the class will have. Let us decide that each person has a name and an age. It feels natural to represent the name as a String and the age as an integer. Let us add this to our schematics:

```java
public class Person {
    private String name;
    private int age;
}
```

Above, we defined that all instances created from the `Person` class have a name and an age. Defining attributes is done in a quite similar fashion as with normal variables. In this case though, there is the keyword `private` in front. This keyword means that `name` and `age` will not show outside of the object, but are instead hidden within it. Hiding things within an object is called *encapsulation*.

Variables defined within a class are called object *attributes*, *object fields* or *object variables*. A beloved child has many names.

So, we have defined the schematics -- the class -- for the person object. All person objects have the variables `name` and `age`. The 'state' of the objects is determined by the values that have been set to its variables.

### Defining your own class - constructor, or "formatting the state"

When an object is created its starting state is defined at the same time. Self-defined objects are created for the most part in the same way as ready-made objects (`ArrayList` objects for example) are created. Objects are created with the `new` command. When creating an object it would be handy to be able to set the values of some of the variables of that object.

```java
    public static void main(String[] args) {
        Person bob = new Person("Bob");
        // ...
    }
```

This can be achieved by defining the method that creates the object, the *constructor*. The constructor for the `Person` class that creates a new `Person` object has been defined in the following example. In the constructor, the person that is being created gets 0 as her age and her name is received from the parameter of the constructor.

```java
public class Person {
    private String name;
    private int age;

    public Person(String initialName) {
        this.age = 0;
        this.name = initialName;
    }
}
```

The constructor always has the same name as the class. In the code above, the class is `Person` and the constructor is `public Person(String initialName)`. The value the constructor receives as a parameter is in parentheses after the name of the constructor. You can imagine the constructor as a method that Java runs when an object is created with the command `new Person("Bob");` Whenever an object is created from a class, the constructor of that class is called.

A few notes: within the constructor there is a command `this.age = 0`. Through it, we set a value for this particular object; we define the internal variable age of "this" object. Another command we use is `this.name = initialName;`. Again, we give the internal variable called name the String that is defined in the constructor. The variables `age` and `name` are automatically visible in the constructor and elsewhere in the object. They are referred to with the this prefix. Due to the `private` modifier, the variables cannot be seen from outside the object.

One more thing: if the programmer does not create a constructor for her class, Java will automatically create a default constructor for it. A default constructor is a constructor that does nothing. So, if you for some reason do not need a constructor you do not need to write one.

### Class definition - methods

We already know how to create and initialize objects. However, objects are useless if they cannot do anything. Therefore, objects should have methods. Let us add to the Person class a method that prints the object on the screen:

```java
public class Person {
    private String name;
    private int age;

    public Person(String nameAtStart) {
        this.age = 0;
        this.name = nameAtStart;
    }

    public void printPerson() {
        System.out.println(this.name + ", age " + this.age + " years");
    }
}
```

As seen above, the method is written within the class. The method name is prefixed with `public void` since it is assumed that users of the object should be capable of using the method and the method should not return anything. With objects the keyword `static` is not used in method definitions. Next week, we will clarify the reason behind that.

Inside the method `printPerson`, there is a single line of code that uses the object variables `name` and `age`. The prefix `this` is used to emphasize that we are referring to the name and age of *this* object. All the object variables are visible from all the methods of the object.

Let us create three persons and ask them to print themselves:

```java
public class Main {

    public static void main(String[] args) {
        Person pekka = new Person("Pekka");
        Person brian = new Person("Brian");
        Person martin = new Person("Martin");

        pekka.printPerson();
        brian.printPerson();
        martin.printPerson();
    }
}
```

The output is:

```output
Pekka, age 0 years
Brian, age 0 years
Martin, age 0 years
```

{% include_relative exercises/002.md %}
{: .exercises }

### More methods

Let us create a method that can be used to increase the age of a person by one:

```java
public class Person {
    // ...

    public void becomeOlder() {
        this.age++;;    // same as this.age = this.age + 1;
    }
}
```

As expected, the method is written inside the class `Person`. The method increases the value of object variable `age` by one.

Let us call the method and see what happens:

```java
public class Main {

    public static void main(String[] args) {
        Person pekka = new Person("Pekka");
        Person andrew = new Person("Andrew");

        pekka.printPerson();
        andrew.printPerson();

        System.out.println("");

        pekka.becomeOlder();
        pekka.becomeOlder();

        pekka.printPerson();
        andrew.printPerson();
    }
}
```

Output:

```output
Pekka, age 0 years
Andrew, age 0 years

Pekka, age 2 years
Andrew, age 0 years
```

When born, both objects have age 0 due to the line `this.age = 0;` in the constructor. The method `becomeOlder` of object `pekka` is called twice. As the output shows, this causes the age of `pekka` to increase by two. It should be noted that when the method `becomeOlder` is called in the object `pekka`, the other object `andrew` is not touched at all and he remains at age 0. The state of an object is independent of the other objects!

Also, the object methods can return a value to the caller of the method. Let us define a method that can be used to ask for the age of a person:

```java
public class Person {
    // ...

    public int getAge() {
        return this.age;
    }
}
```

Now the `void` in the method definition is replaced with `int` since the value the method returns has the type integer. The following example demonstrates, how the value returned by a method can be used:

```java
public class Main {

    public static void main(String[] args) {
        Person pekka = new Person("Pekka");
        Person andrew = new Person("Andrew");

        pekka.becomeOlder();
        pekka.becomeOlder();

        andrew.becomeOlder();

        System.out.println( "Age of Pekka: "+pekka.getAge() );
        System.out.println( "Age of Andrew: "+andrew.getAge() );

        int total = pekka.getAge() + andrew.getAge();

        System.out.println( "Pekka and Andrew total of "+total+ " years old" );
    }
}
```

Output:

```output
Age of Pekka: 2
Age of Andrew: 1

Pekka and Andrew total of 3 years old
```

{% include_relative exercises/003.md %}
{% include_relative exercises/004.md %}
{% include_relative exercises/005.md %}
{: .exercises }

### The Person class grows

Let us get back to work on the `Person` class. The current version of the class looks like this:

```java
public class Person {
    private String name;
    private int age;

    public Person(String initialName) {
        this.age = 0;
        this.name = initialName;
    }

    public void printPerson() {
        System.out.println(this.name + ", age " + this.age + " years");
    }

    public void becomeOlder() {
        this.age = this.age + 1;
    }
}
```

Let us create a method for person that can figure out if a person is an adult. The method returns a boolean -- either `true` or `false`:

```java
public class Person {
    // ...

    public boolean isAdult(){
        if ( this.age < 18 ) {
            return false;
        }

        return true;
    }

   /*
      note that the method could also be written like this:
  
      public boolean isAdult(){
        return this.age >= 18;
      }
   */
}
```

Let us test it:

```java
    public static void main(String[] args) {
        Person bob = new Person("Bob");
        Person andy = new Person("Andy");

        int i = 0;
        while ( i < 30 ) {
            bob.becomeOlder();
            i++;
        }

        andy.becomeOlder();

        System.out.println("");

        if ( andy.isAdult() ) {
            System.out.print("adult: ");
            andy.printPerson();
        } else {
            System.out.print("minor: ");
            andy.printPerson();
        }

        if ( bob.isAdult() ) {
            System.out.print("adult: ");
            bob.printPerson();
        } else {
            System.out.print("minor: ");
            bob.printPerson();
        }
    }
```

```output
minor: Andy, age 1 years
adult: bob, age 30 years
```

Let us tune up the solution a little further. Now, a person can only be printed in a manner where in addition to the name, the age also gets printed. In some cases, we might only want to print the name of the object. Let us tailor a method for this purpose:

```java
public class Person {
    // ...

    public String getName() {
        return this.name;
    }
}
```

The method `getName` returns the object variable `name` to its caller. The name of the method might seem a little odd (or not). In Java, it is considered the 'correct' way to name an object-variable-returning method in this manner; as `getVariableName`. Methods like these are often called 'getters'.

Let us edit the main program to use the new 'getter':

```java
    public static void main(String[] args) {
        Person bob = new Person("bob");
        Person andy = new Person("andy");

        int i = 0;
        while ( i < 30 ) {
            bob.becomeOlder();
            i++;
        }

        andy.becomeOlder();

        System.out.println("");

        if ( andy.isAdult() ) {
            System.out.println( andy.getName() + " is an adult" );
        } else {
            System.out.println( andy.getName() + " is a minor" );
        }

        if ( bob.isAdult() ) {
            System.out.println( bob.getName() + " is an adult" );
        } else {
            System.out.println( bob.getName() + " is a minor" );
        }
    }
```

The print is starting to look pretty clean:

```output
andy is a minor
bob is an adult
```

### toString

We have been guilty of bad programming style; we have created a method that prints an object, `printPerson`. The recommended way of doing this is by defining a method that returns a "character string representation" of the object. In Java, a method returning a `String` representation is called `toString`. Let us define this method for person:

```java
public class Person {
    // ...

    public String toString() {
        return this.name + ", age " + this.age + " years";
    }
}
```

The method `toString` works just like `printPerson`, but instead of printing it the method returns the string representation. The call to the method can be used for printing it if necessary.

The method is used in a slightly surprising way:

```java
    public static void main(String[] args) {
        Person bob = new Person("Bob");
        Person andy = new Person("Andy");

        int i = 0;
        while ( i < 30 ) {
            bob.becomeOlder();
            i++;
        }

        andy.becomeOlder();

        System.out.println( andy ); // same as System.out.println( andy.toString() ); 
        System.out.println( bob ); // same as System.out.println( bob.toString() ); 
    }
```

The principle is that the `System.out.println` method requests the string representation of an object and then prints it. The returned string representation of the `toString` method does not have to be written, as Java adds it automatically. When the programmer writes:

```java
        System.out.println( andy );
```

Java completes the call during runtime to the format:

```java
        System.out.println( andy.toString() );
```

What happens is that the object is asked for its string representation. The string representation the object is returned and is printed normally with the `System.out.println` command.

**We can get rid of the obsolete `printObject` method.**

{% include_relative exercises/006.md %}
{: .exercises }

### More methods

Let us continue with the class `Person`. We would be interested in knowing the [body mass index](http://en.wikipedia.org/wiki/Body_mass_index) of a person. To calculate the index, we need to know the height and weight of the person. We add for both height and weight object variables and methods that can be used to assign the variables a value. When this is in place, we add a method that calculates the body mass index.

Here is the class `Person` after the changes (only the parts affected by the change are shown):

```java
public class Person {
    private String name;
    private int age;
    private int weight;
    private int height;

    public Person(String initialName) {
        this.age = 0;
        this.name = initialName;
        this.weight = 0;
        this.height = 0;
    }

    public void setHeight(int newHeight) {
        this.height = newHeight;
    }

    public void setWeight(int newWeight) {
        this.weight = newWeight;
    }

    public double bodyMassIndex(){
        double heightDividedByHundred = this.height / 100.0;
        return this.weight / ( heightDividedByHundred * heightDividedByHundred );
    }

    // ...
}
```

We added object variables `height` and `weight`, and methods `setHeight` and `setWeight` that can be used to give values to the variables. In naming the methods, we follow the Java convention to call a method that just sets a new value to a variable `setVariableName`. This type of methods are usually called *setter methods*.

The new methods in use:

```java
public static void main(String[] args) {
    Person matti = new Person("Matti");
    Person john = new Person("John");

    matti.setHeight(180);
    matti.setWeight(86);

    john.setHeight(175);
    john.setWeight(64);

    System.out.println(matti.getName() + ", body mass index: " + matti.bodyMassIndex());
    System.out.println(john.getName() + ", body mass index: " + john.bodyMassIndex());
}
```

The output:

```output
Matti, body mass index: on 26.54320987654321
John, body mass index: on 20.897959183673468
```

### Object variable and parameter with identical name

Above, the method setHeight assigns the object variable height the value of the parameter `newHeight`:

```java
public void setHeight(int newHeight) {
    this.height = newHeight;
}
```

The parameter could also be named identically with the object variable:

```java
public void setHeight(int height) {
    this.height = height;
}
```

Now, the name height means the parameter `height` and the identically named object variable is referred to as `this.height`. The following would not work since the object variable `height` is not at all referred to in the code:

```java
public void setHeight(int height) {
    // DOES NOT WORK!
    height = height;
    // this just assigns the value of the parameter to the parameter itself
}
```

### Contolling the number of decimals when printing a float

The number of decimals in the last output was far too high, two decimals would be enough. One technique to control how a float number is printed is to use the command `String.format`.

If value is a float number, the command `String.value( "%.2f", value )` returns a string where the value is rounded to contain 2 decimals. The number between dot and f defines the amount of decimals shown.

After changing the code, we have the following:

```java
System.out.println(matti.getName() + ", body mass index: " + String.format( "%.2f", matti.bodyMassIndex()));
System.out.println(john.getName() + ", body mass index: " + String.format( "%.2f", john.bodyMassIndex()));
```

The output is:

```output
Matti,  body mass index: 26,54
John,  body mass index: 20,90
```

The method `String.format` is not the most flexible way provided by Java for formatting float values, but it is simple to use and suits our purposes here well.

{% include_relative exercises/007.md %}
{: .exercises }

## Important notes regarding the use of objects. You should definately read these.

Object-oriented programming is mostly about turning concepts into their own entities, or in other words forming abstractions. One might think that it is pointless to create an object that only holds one number in it, and that the same could be achieved with simple `int` variables. This is not the case. If a clock consists of just 3 int variables that are then increased, the program loses some human readability. It becomes more difficult to "see" what the program is about. Earlier in the material we mentioned the advice of the renown programmer Kent Beck: *"Any fool can write code that a computer can understand. Good programmers write code that humans can understand"*, since the hand of a clock is its own clearly definable concept, it is a good idea to create it an own class - `BoundedCounter` - for the sake of human readability.

Turning a concept into a class of its own is a good idea for a lot of reasons. Firstly, some details (i.e. when the counter makes a full round) can be hidden inside the class (*abstracted*). Instead of writing an if-clause and an assignment operation, it is enough that the user of the counter calls the descriptively named method `next()`. In addition to clocks, the created counter might be good for being used as a building block for other projects too, so a class made from a clear concept can be very versatile. Another huge advantage we gain by writing code this way, is that when the details of the mechanics are hidden, they can be changed if need be.

We established that a clock contains three hands, it consists of three concepts. Actually the clock itself is a concept too and next week we will make the class Clock. Then, we can create distinct Clock objects. Clock will be an object which functionality is based on "simpler" objects, the hands. This is the grand idea of object-oriented programming: a program is built out of small, clearly defined co-operating objects.

Now, we will take some careful first steps in the object world. Towards the end of the course, objects will start to come to you naturally and the idea of programs being built out of small, well defined, co-operating pieces - which at this point might feel incomprehensible - will become something you will take for granted.

### 21.13 Calling other methods within an object

Objects can also call its own methods. Let us assume we would like to include body mass index in the string representation of the person objects. Instead of calculating the body mass index in the toString method, a better idea is to call the method `bodyMassIndex` from the `toString` method:

```java
public String toString() {
    return this.name + ", age " + this.age + " years, my body mass index is " + this.bodyMassIndex();
}
```

As can be seen, an object can call its own method by prefixing the method name with `this` and dot. The this is not necessary, so also the following works:

```java
public String toString() {
    return this.name + ", age " + this.age + " years, my body mass index is " + bodyMassIndex();
}
```

Now it is time to continue practising programming.

{% include_relative exercises/008.md %}
{: .exercises }