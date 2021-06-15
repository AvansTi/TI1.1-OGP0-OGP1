---
layout: default
title: Constructors
meta: 
todo: merge with more information on constructors
---
{% include licence.md %}

## Multiple constructors

Let us return to the class that handles Persons again. The class `Person` currently looks like this:

```java
public class Person {

    private String name;
    private int age;
    private int height;
    private int weight;

     public Person(String name) {
        this.name = name;
        this.age = 0;
        this.weight = 0;
        this.height = 0;
    }

    public void printPerson() {
        System.out.println(this.name + " I am " + this.age + " years old");
    }

    public void becomeOlder() {
        this.age++;
    }

    public boolean adult(){
        if ( this.age < 18 ) {
            return false;
        }

        return true;
    }

    public double weightIndex(){
        double heightInMeters = this.height/100.0;

        return this.weight / (heightInMeters*heightInMeters);
    }

    public String toString(){
        return this.name + " I am " + this.age + " years old, my weight index is " + this.weightIndex();
    }

    public void setHeight(int height){
        this.height = height;
    }

    public int getHeight(){
        return this.height;
    }

    public int getWeight() {
        return this.weight;
    }

    public void setWeight(int weight) {
        this.weight = weight;
    }

    public String getName(){
        return this.name;
    }
}
```

All person objects are 0 years old at creation, since the constructor sets it to 0:

```java
public Person(String name) {
    this.name = name;
    this.age = 0;
    this.weight = 0;
    this.height = 0;
}
```

We also want to create a person so that in addition to name, can be given an age as a parameter. This can be achieved easily, since multiple constructors can exist. Let us make an alternative constructor. You do not need to remove the old one.

```java
public Person(String name) {
    this.name = name;
    this.age = 0;
    this.weight = 0;
    this.height = 0;
}

public Person(String name, int age) {
    this.name = name;
    this.age = age;
    this.weight = 0;
    this.height = 0;
}
```

Now, creating objects can be done in two different ways:

```java
public static void main(String[] args) {
    Person pekka = new Person("Pekka", 24);
    Person esko = new Person("Esko");

    System.out.println( pekka );
    System.out.println( esko );
}
```

```output
Pekka, age 24 years
Esko, age 0 years
```

The technique in which a class has two constructors is called *constructor overloading*. A class can have multiple constructors, which are different from one another according to parameter quanitities and/or types. However, it is not possible to create two different constructors that have exactly the same type of parameters. We cannot add a constructor `public Person(String name, int weight)` on top of the old ones, since it is impossible for Java to tell the difference between this one and the one in which the integer stands for the age.

### Calling your own constructor

But wait, in chapter 21 we noted that "copy-paste" code is not too great of an idea! When we inspect the overloaded constructors above, we notice that they have the same code repeated in them. We are not ok with *this*.

The old constructor actually is a special case of the new constructor. What if the old constructor could 'call' the new constructor? This can be done, since you can call another constructor from within a constructor with this!

Let us change the old constructor that does nothing, but only calls the new constructor below it and asks it to set the age to 0:

```java
public Person(String name) {
    this(name, 0);  // run here the other constructor's code and set the age parameter to 0
}

public Person(String name, int age) {
    this.name = name;
    this.age = age;
    this.weight = 0;
    this.height = 0;
}
```

Calling the own constructor of a class `this(name, 0);` might seem a little peculiar. But we can imagine that during the call it will automatically copy-paste the code from the constructor below and that 0 is entered to the age parameter.

### Overloading a method

Just like constructors, methods can also be overloaded and multiple versions of a method can exist. Again, the parameter types of different versions have to be different. Let us create another version of the `becomeOlder`, which enables aging the person the amount of years that is entered as a parameter:

```java
public void becomeOlder() {
    this.age = this.age + 1;
}

public void becomeOlder(int years) {
    this.age = this.age + years;
}
```

In the following, "Pekka" is born as a 24-year old, ages one year, and then 10:

```java
public static void main(String[] args) {
    Person pekka = new Person("Pekka", 24);

    System.out.println(pekka);
    pekka.becomeOlder();
    System.out.println(pekka);
    pekka.becomeOlder(10);
    System.out.println(pekka);
}
```

Prints:

```output
Pekka, age 24 years
Pekka, age 25 years
Pekka, age 35 years
```

Now, a person has two `becomeOlder` methods. The method that is chosen to be run depends on the amount of parameters entered in to the method call. The method `becomeOlder` can also be run through the method `becomeOlder(int years)`:

```java
public void becomeOlder() {
    this.becomeOlder(1);
}

public void becomeOlder(int years) {
    this.age = this.age + years;
}
```

{% include_relative exercises/001.md %}
{: .exercises }