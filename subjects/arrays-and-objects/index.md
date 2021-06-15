---
layout: default
title: Arrays and Objects
meta: Put extra info here, like if there any subjects required for this subject
todo: what should be improved in this chapter
---
{% include licence.md %}

## About arrays and objects
If need be, any type of object can be put into an array. In the following, an example of an array into which will be put Person objects:

```java
public static void main(String[] args) {
    Person[] persons = new Person[3];

    persons[0] = new Person("Pekka");
    persons[1] = new Person("Antti");
    persons[2] = new Person("Juhana");

    for ( int i=0; i < 30; i++ ) {
        persons[0].becomeOlder();
        persons[1].becomeOlder();
        persons[2].becomeOlder();
    }

    for ( Person person : persons ) {
        reportMaturity(person);
    }
}
```

First we create an array that can hold 3 Person objects. We put Pekka in slot 0, Antti in 1 and Juhana in 2. We age all by 30 years and check all of their matureness with the help of the method from the previous chapter.

The same example with ArrayLists:

```java
public static void main(String[] args) {
    ArrayList<Person> persons = new ArrayList<Person>();

    persons.add( new Person("Pekka") );
    persons.add( new Person("Antti") );
    persons.add( new Person("Juhana") );

    for ( int i=0; i < 30; i++ ) {
        for ( Person person : persons ) {
            person.becomeOlder();
        }

        //  or persons.get(0).becomeOlder();
        //     persons.get(1).becomeOlder();
        //     ...
    }

    for ( Person person : persons ) {
        reportMaturity(person);
    }
}
```

In most situations it's better to use ArrayList instead of an array. However there can be cases where an array is adequate and is simpler to use.

A week always consists of seven days. It would be meaningful to form it out of exactly 7 Day objects. Since there's always 7 Day objects, an array will suit the situation very well:

```java
public class Day {
    private String name;
    // ...
}

public class Week {
    private Day[] days;

    public Week(){
        days = new Day[7];
        days[0] = new Day("Monday");
        days[1] = new Day("Tuesday");
        // ...
    }
}
```