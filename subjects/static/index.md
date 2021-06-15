---
layout: default
title: Static
meta: Put extra info here, like if there any subjects required for this subject
todo: what should be improved in this chapter
---
{% include licence.md %}

## To static or not to static?

When we started using objects, the material advised to leave out the keyword 'static' when defining their methods. However, up until week 3 all of the methods included that keyword. So what is it all about?

The following example has a method `resetArray`, that works as its name implies; it sets all of the cells of an array that it receives as a parameter to 0.

```java
public class Program {

    public static void resetArray(int[] table) {
        for ( int i=0; i < table.length; i++ )
            table[i] = 0;
    }

    public static void main(String[] args) {
        int[] values = { 1, 2, 3, 4, 5 };

        for ( int number : values ) {
            System.out.print( number + " " );  // prints 1, 2, 3, 4, 5
        }

        System.out.println();

        resetArray(values);

        for ( int number : values ) {
            System.out.print( number + " " );  // prints 0, 0, 0, 0, 0
        }
    }
}
```

We notice that the method definition now has the keyword `static`. The reason for that is that the method does not operate on any object, instead it is a *class method* or in other words static methods. In contrast to instance methods, static methods are not connected to any particular object and thus the reference `this` is not valid within static methods. A static method can operate only with data that is given it as parameter. The parameter of a static method can naturally be an object.

Since static methods are not connected to any object, those can not be called through the object name: `objectName.methodName()` but should be called as in the above example by using only the method name.

If the static method is called from a different class, the call is of the form `ClassName.staticMethodName()`. The below example demonstrates that:

```java
public class Program {
    public static void main(String[] args) {
        int[] values = { 1, 2, 3, 4, 5 };

        for ( int value : values ) {
            System.out.print( value + " " );  // prints: 1, 2, 3, 4, 5
        }

        System.out.println();

        ArrayHandling.resetArray(values);

        for ( int value : values ) {
            System.out.print( value + " " );  // prints: 0, 0, 0, 0, 0
        }
    }
}
public class ArrayHandling {
    public static void resetArray(int[] array) {
        for ( int i=0; i < array.length; i++ ) {
            array[i] = 0;
        }
    }
}
```

The static method that has been defined within another class will now be called with `ArrayHandling.resetArray(parameter);`.

## When static methods should be used

All object state-handling methods should be defined as normal object methods. For example, all of the methods of the `Person`, `MyDate`, `Clock`, `Team`, ... classes we defined during the previous weeks should be defined as normal object methods, not as statics.

Lets get back to the `Person` class yet again. In the following is a part of the class definition. All of the object variables are referred to with the `this` keyword because we emphasize that we are handling the object variables 'within' the said object..

```java
public class Person {
    private String name;
    private int age;

    public Person(String name) {
        this.age = 0;
        this.name = name;
    }

    public boolean isAdult(){
        if ( this.age < 18 ) {
            return false;
        }

        return true;
    }

    public void becomeOlder() {
        this.age++;
    }

    public String getName() {
        return this.name;
    }
}
```

Because the methods manipulate the object, they do not need to be defined as `static`, or in other words "not belonging to the object". If we try to do this, the program won't work:

```java
public class Person {
    //...

    public static void becomeOlder() {
        this.age++;
    }
}
```

As a result we'll get an error **`non-static variable age can not be referenced from static context`**, which means that a static method cannot handle an object method.

So when should a static method be used then? Let us inspect the object `Person` handling an example familiar from chapter 23:

```java
public class Program {
    public static void main(String[] args) {
        Person pekka = new Person("Pekka");
        Person antti = new Person("Antti");
        Person juhana = new Person("Juhana");

        for ( int i=0; i < 30; i++ ) {
            pekka.becomeOlder();
            juhana.becomeOlder();
        }

        antti.becomeOlder();

        if ( antti.isAdult() ) {
            System.out.println( antti.getName() + " is an adult" );
        } else {
            System.out.println( antti.getName() + " is a minor" );
        }

        if ( pekka.isAdult() ) {
            System.out.println( pekka.getName() + " is an adult" );
        } else {
            System.out.println( pekka.getName() + " is a minor" );
        }

        if ( juhana.isAdult() ) {
            System.out.println( juhana.getName() + " is an adult" );
        } else {
            System.out.println( juhana.getName() + " is a minor" );
        }
    }
}
```

We'll notice that the piece of code that reports the matureness of persons is copy-pasted twice in the program. It looks really bad!

Reporting the maturity of a person is an excellent candidate for a static method. Let's rewrite the Program using that method:

```java
public class Main {

    public static void main(String[] args) {
        Person pekka = new Person("Pekka");
        Person antti = new Person("Antti");
        Person juhana = new Person("Juhana");

        for ( int i=0; i < 30; i++ ) {
            pekka.becomeOlder();
            juhana.becomeOlder();
        }

        antti.becomeOlder();

        reportMaturity(antti);

        reportMaturity(pekka);

        reportMaturity(juhana);
    }

    private static void reportMaturity(Person person) {
        if ( person.isAdult() ) {
            System.out.println(person.getName() + " is an adult");
        } else {
            System.out.println(person.getName() + " is a minor");
        }
    }
}
```

The method `reportMaturity` is defined as static so it doesn't belong to any object, **but** the method receives a `Person` object as a parameter. The method is not defined within the Person-class since even though it handles a Person object that it receives as a parameter, it is an assistance method of the main program we just wrote. With the method we've made main more readable.

{% include_relative exercises/001.md %}
{: .exercises }
