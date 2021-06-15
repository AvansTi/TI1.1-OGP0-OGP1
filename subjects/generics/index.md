---
layout: ogp1
title: Generics
meta: 
todo: 
---
{% include licence.md %}

## Generics

We speak about *Generics* in connection to the way classes can conserve objects of genric type. Generics is based on the generic type parameter which is used when we define a class, and which helps us to define the types that have to be chosen when an *object is created*. A class generics can be defined by setting up the number of type parameters we want. This number is written after the class name and between the greater-than and less-than signs. We now implement our own generic class `Slot` which be assigned whatever object.

```java
public class Slot<T> {
    private T key;

    public void setValue(T key) {
        this.key = key;
    }

    public T getValue() {
        return key;
    }
}
```

The definition `public class Slot<T>` tells us that we have to give a type parameter to the constructor of the class `Slot`. After the constructor call the object variables have to be the same type as what established with the call. We now create a slot which memorizes strings.

```java
Slot<String> string = new Slot<String>();
string.setValue(":)");

System.out.println(string.getValue());
```

```output
:)
```

If we change the type parameter we can create different kinds of `Slot` ojects, whose purpose is to memorize objects. For instance, we can memorize an integer in the following way:

```java
Slot<Integer> num = new Slot<Integer>();
num.setValue(5);

System.out.println(slot.getValue());
```

```output
5
```

An important part of Java data structures are programmed to be generic. For instance, `ArrayList` receives one parameter, `HashMap` two.

```java
List<String> string = new ArrayList<String>();
Map<String, String> keyCouples = new HashMap<String, String>();
```

In the future, when you see the type `ArrayList<String>`, for instance, you know that its internal structure makes use of a generic type parameter.

### The Interface which Makes Use of Generics: Comparable

In addition to normal interfaces, Java has interfaces which make use of generics. The internal value types of generic interfaces are defined in the same way as for generic classes. Let us have a look at Java made-up [Comparable](http://java.sun.com/javase/8/docs/api/java/lang/Comparable.html) interface. The `Comparable` interface defines the `compareTo` method, which returns the place of `this` object, in relation to the parameter object (a negative number, 0, or a positive number). If this object is placed before the parameter object in the comparison order, the method returns a negative value, whereas it returns a positive value if it is placed after the parameter object. If the objects are placed at the same place in the comparison order, the method returns 0. With comparison order we mean the object order of magnitude defined by the programmer, i.e. the object order, when they are sorted with the sort method.

One of the advantages of the interface `Comparable` is that it allows us to sort a list of `Comparable` type keys by using the standard library method `Collections.sort`, for instance. `Collections.sort` uses the method `compareTo` of a key list to define in which order these keys should be. We call Natural Ordering this ordering technique which makes use of the `compareTo` method.

We create the class `ClubMember`, which depicts the young people and children who belong to the club. The members have to eat in order of height, so the club members will implement the interface `Comparable`. The interface `Comparable` also takes as type parameter the class which it is compared to. As type parameter, we use the `ClubMember` class.

```java
public class ClubMember implements Comparable<ClubMember> {
    private String name;
    private int height;

    public ClubMember(String name, int height) {
        this.name = name;
        this.height = height;
    }

    public String getName() {
        return this.name;
    }

    public int getHeight() {
        return this.height;
    }

    @Override
    public String toString() {
        return this.getName() + " (" + this.getHeight() + ")";
    }

    @Override
    public int compareTo(ClubMember clubMember) {
        if(this.height == clubMember.getHeight()) {
            return 0;
        } else if (this.height > clubMember.getHeight()) {
            return 1;
        } else {
            return -1;
        }
    }
}
```

The interface requires the method `compareTo`, which returns an integer that tells us the comparison order. Our method `compareTo()` has to return a negative number if `this` object is smaller than its parameter object, or zero, if the two members are equally tall. Therefore, we can implement the above method `compareTo`, in the following way:

```java
@Override
public int compareTo(ClubMember clubMember) {
    return this.height - clubMember.getHeight();
}
```

Sorting club members is easy, now.

```java
List<ClubMember> clubMembers = new ArrayList<ClubMember>();
clubMembers.add(new ClubMember("mikael", 182));
clubMembers.add(new ClubMember("matti", 187));
clubMembers.add(new ClubMember("joel", 184));

System.out.println(clubMembers);
Collections.sort(clubMembers);
System.out.println(clubMembers);
```

```output
[mikael (182), matti (187), joel (184)]
[mikael (182), joel (184), matti (187)]
```

If we want to sort the members in descending order, we only have to switch the variable order in our `compareTo` method.

{% include_relative exercises/001.md %}
{% include_relative exercises/002.md %}
{% include_relative exercises/003.md %}
{: .exercises }
