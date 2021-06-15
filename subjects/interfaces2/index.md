---
layout: ogp1
title: Many Interfaces
meta: Put extra info here, like if there any subjects required for this subject
todo: what should be improved in this chapter
---
{% include licence.md %}

## Many Interfaces, and Interface Flexibility

Last week we were introduced to interfaces. An interface defines one or more methods which have to be implemented in the class which implements the interface. The interfaces can be stored into packages like any other class. For instance, the interface `Identifiable` below is located in the package `application.domain`, and it defines that the classes which implement it have to implement the method `public String getID()`.

```java
package application.domain;

public interface Identifiable {
    String getID();
}
```

The class makes use of the interface through the keyword `implements`. The class `Person`, which implements the `Idenfifiable` interface. The `getIDof` Person class always returns the person ID.

```java
package application.domain;

public class Person implements Identifiable {
    private String name;
    private String id;

    public Person(String name, String id) {
        this.name = name;
        this.id = id;
    }

    public String getName() {
        return this.name;
    }

    public String getPersonID() {
        return this.id;
    }

    @Override
    public String getID() {
        return getPersonID();
    }

    @Override
    public String toString(){
        return this.name + " ID: " +this.id;
    }
}
```

An interface strength is that interfaces are also *types*. All the objects which are created from classes that implement an interface also have that interface's type. This effictively helps us to build our applications.

We create the class `Register`, which we can use to search for people against their names. In addition to retrieve single people, `Register` provides a method to retrieve a list with all the people.

```java
public class Register {
    private HashMap<String, Identifiable> registered;

    public Register() {
        this.registered = new HashMap<String, Identifiable>();
    }

    public void add(Identifiable toBeAdded) {
        this.registered.put(toBeAdded.getID(), toBeAdded);
    }

    public Identifiable get(String id) {
        return this.registered.get(id);
    }

    public List<Identifiable> getAll() {
        return new ArrayList<Identifiable>(registered.values());
    }
}
```

Using the register is easy.

```java
Register personnel = new Register();
personnel.add( new Person("Pekka", "221078-123X") );
personnel.add( new Person("Jukka", "110956-326B") );

System.out.println( personnel.get("280283-111A") );

Person found = (Person) personnel.get("110956-326B");
System.out.println( found.getName() );
```

Because the people are recorded in the register as `Identifiable`, we have to change back their type if we want to deal with people through those methods which are not defined in the interface. This is what happens in the last two lines.

What about if we wanted an operation which returns the people recorded in our register sorted according to their ID?

One class can implement various different interfaces, and our `Person` class can implement `Comparable` in addition to `Identifiable`. When we implement various different interfaces, we separate them with a comma `(public class ... implements FirstInterface, SecondInterface ...)`. When we implement many interfaces, we have to implement all the methods required by all the interfaces. Below, we implement the interface `Comparable` in the class `Person`.

```java
package application.domain;

public class Person implements Identifiable, Comparable<Person> {
    private String name;
    private String id;

    public Person(String name, String id) {
        this.name = name;
        this.id = id;
    }

    public String getName() {
        return this.name;
    }

    public String getPersonID() {
        return this.id;
    }

    @Override
    public String getID() {
        return getPersonID();
    }

    @Override
    public int compareTo(Person another) {
        return this.getID().compareTo(another.getID());
    }
}
```

Now, we can add to the register method `sortAndGetEverything`:

```java
    public List<Identifiable> sortAndGetEverything() {
        ArrayList<Identifiable> all = new ArrayList<Identifiable>(registered.values());
        Collections.sort(all);
        return all;
    }
```

However, we notice that our solution does not work. Because the people are recorded into the register as if their type was Identifiable, `Person` has to implement the interface `Comparable<Identifiable>` so that our register could sort people with its method `Collections.sort()`. This means we have to modify Person's interface:

```java
public class Person implements Identifiable, Comparable<Identifiable> {
    // ...

    @Override
    public int compareTo(Identifiable another) {
        return this.getID().compareTo(another.getID());
    }
}
```

Now our solution works!

Our Register is unaware of the real type of the objects we record. We can use the class Register to record objects of different types than `Person`, as long as the object class implements the interface `Identifiable`. For instance, below we use the register to manage shop sales:

```java
public class Sale implements Identifiable {
    private String name;
    private String barcode;
    private int stockBalance;
    private int price;

    public Sale(String name, String barcode) {
        this.name = name;
        this.barcode = barcode;
    }

    public String getID() {
        return barcode;
    }

    // ...
}

Register products = new Register();
products.add( new Product("milk", "11111111") );
products.add( new Product("yogurt", "11111112") );
products.add( new Product("cheese", "11111113") );

System.out.println( products.get("99999999") );

Product product = (Product)products.get("11111112");
product.increaseStock(100);
product.changePrice(23);
```

The class `Register` is quite universal now that it is not dependent on concrete classes. Whatever class which implements `Identifiable` is compatible with `Register`. However, the method `sortAndGetEverything` can only work if we implement the interface `Comparable<Identifiable>`.

### IntelliJ Tips
>* All IntelliJ tips can be found [here](https://avansti.github.io/TI1.1-OGP0-OGP1-Lesmateriaal/intellij)
>* **Implement all abstract methods**
>Let us suppose that your program contains the interface `Interface`, and you are building the class `Class` which implements the>interface. It will be annoying to write the declaration raws of all the interface methods.
>
>However it is possible to ask IntelliJ to fill in the method bodies automatically. When you have defined the interface a class should implement, i.e. when you have written
>
>```java
>public class Class implements Interface {
>}
>```
>
>IntelliJ paints the class name red. If you go to lamp icon on the left corner of the raw, click, and choose *Implement all abstract methods*, the method bodies will appear in your code!
>* **Clean and Build**
>Sometimes, IntelliJ may get confused and try to run a code version without noticing all the corrected changes made to it. Usually  you notice it because something "strange" happens. Usually, you can fix the problem by using *Rebuild* operation. The operation is found in the *Build* menu. Rebuild deletes the translated versions of the code and generates a new translation.
>{: .tip}

{% include_relative exercises/001.md %}
{: .exercises }
