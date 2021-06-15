---
layout: ogp1
title: Interfaces
meta: Put extra info here, like if there any subjects required for this subject
todo: what should be improved in this chapter
---
{% include licence.md %}

## Interfaces

`Interface` is an instrument we have to define the functionality our classes should have. Interfaces are defined as normal Java classes, but instead of the definition "`public class` ...", we write "`public interface` ...". The interfaces influence class behaviour by defining the method names and return values, but they *do* **not** *contain method implementation*. The access modifier is not specified, because it is always `public`. Let us have a look at the interface `Readable`, which defines whether an object can be read.

```java
public interface Readable {
    String read();
}
```
            
The interface `Readable` defines the method `read()`, which returns a string object. The classes which implement an interface decide *in which way* the methods defined in the interface have to be implemented, in the end. A class *implements* an interface by adding the keyword implements between the class and the interface name. Below, we create the class `SMS` which implements `Readable` interface.

```java
public class SMS implements Readable {
    private String sender;
    private String content;

    public SMS(String sender, String content) {
        this.sender = sender;
        this.content = content;
    }

    public String getSender() {
        return this.sender;
    }

    public String read() {
        return this.content;
    }
}
```

Because the class `SMS` implements the interface `Readable` (`public class SMS implements Readable`), the class `SMS` must implement the method `public String read()`. The implementations of methods defined in the interface must always have public access.

*An interface is a behavioural agreement. In order to implement the behaviour, the class must implement the methods defined by the interface. The programmer of a class which implements an interface has to define what the behaviour will be like. Implementing an interface means to agree that the class will offer all the actions defined by the interface, i.e. the behaviour defined by the interface. A class which implements an interface but does not implement some of the interface methods can not exist.*

Let us implement another class which implements the `Readable` interface, in addition to our `SMS` class. The class `EBook` is the electronic implementation of a book, and it contains the book name and page number. The EBook reads one page at time, and the method`public String read()` always returns the string of the following page.

```java
public class EBook implements Readable {
    private String name;
    private ArrayList<String> pages;
    private int pageNumber;

    public EBook(String name, ArrayList<String> pages) {
        this.name = name;
        this.pages = pages;
        this.pageNumber = 0;
    }

    public String getName() {
        return this.name;
    }

    public int howManyPages() {
        return this.pages.size();
    }

    public String read() {
        String page = this.pages.get(this.pageNumber);
        nextPage();
        return page;
    }

    private void nextPage() {
        this.pageNumber = this.pageNumber + 1;
        if(this.pageNumber % this.pages.size() == 0) {
            this.pageNumber = 0;
        }
    }
}
```

Classes which implement interfaces generate objects as well as normal classes, and they can be used as `ArrayList` types too.

```java
    SMS message = new SMS("ope", "Awesome stuff!");
    System.out.println(message.read());

    ArrayList<SMS> messages = new ArrayList<SMS>();
    messages.add(new SMS("unknown number", "I hid the body.");
```

```output
Awesome stuff!
```

```java
    ArrayList<String> pages = new ArrayList<String>();
    pages.add("Split your method into short clear chunks.");
    pages.add("Devide the user interface logic from the application logic.");
    pages.add("At first, always code only a small program which solves only a part of the problem.");
    pages.add("Practice makes perfect. Make up your own fun project.");

    EBook book = new EBook("Programming Hints.", pages);
    for(int page = 0; page < book.howManyPages(); page++) {
        System.out.println(book.read());
    }
```

```output
Split your method into short clear chunks.
Divide the user interface logic from the application logic.
At first, always code only a small program which solves only a part of the problem.
Practice makes perfect. Make up your own fun project.
```

{% include_relative exercises/001.md %}
{: .exercises }

### An Interface as Variable Type

When we create a new variable we always specify its type. There are two types of variable types: primitive-type variables (int, double, ...) and reference-type (all objects). As far as reference-type variables are concerned, their class has also been their type, so far.

```java
    String string = "string-object";
    SMS message = new SMS("teacher", "Something crazy is going to happen");
```

The type of an object can be different from its class. For instance, if a class implements the interface `Readable`, its type is `Readable`, too. For instance, since the class `SMS` implements the interface `Readable`, it has two types: `SMS` and `Readable`.

```java
    SMS message = new SMS("teacher", "Awesome stuff!");
    Readable readable = new SMS("teacher", "The SMS is Readable!");

    ArrayList<String> pages = new ArrayList<String>();
    pages.add("A method can call itself.");

    Readable book = new EBook("Recursion Principles", pages);
    for(int page = 0; page < ((EBook)book).howManyPages(); page++) {
        System.out.println(book.read());
    }
```

Because an interface can be used as type, it is possible to create a list containing interface-type objects.

```java
    ArrayList<Readable> numberList = new ArrayList<Readable>();

    numberList.add(new SMS("teacher", "never been programming before..."));
    numberList.add(new SMS("teacher", "gonna love it i think!"));
    numberList.add(new SMS("teacher", "give me something more challenging! :)"));
    numberList.add(new SMS("teacher", "you think i can do it?"));
    numberList.add(new SMS("teacher", "up here we send several messages each day"));

    for (Readable readable: numberList) {
        System.out.println(readable.read());
    }
```

The class `EBook` implements the interface `Readable`. However, notice that even though the type of the class `EBook` is an interface, `EBook` is not the type of all the classes which implement the `Readable` interface. It is possible to assign an `EBook` object to a `Readable` variable, but the assignment does not work in the opposite way without a particular type change.

```java
    Readable readable = new SMS("teacher", "The SMS is Readable!"); // works
    SMS message = readable; // not possible

    SMS transformedMessage = (SMS) readable; // works
```

Type casting works if and only if the variable's type is really what we try to change it into. Type casting is not usually a best practice; one of the only cases where that is legitimate is in connection with the method `equals`.

### An Interface as Method Parameter

The real use of interfaces becomes clear when we use them for the type of a method parameter. Because interfaces can be used as variable type, they can be used in method calls as parameter type. For instance, the below method print of class `Printer` receives a `Readable` variable.

```java
public class Printer {
    public void print(Readable readable) {
        System.out.println(readable.read());
    }
}
```

The real value of the `print` method of class `Printer` is that its parameter can be *whatever* class instance which implements our `Readable` interface. When we call the method of an object, the method will work regardless of the class of this object, as long as the object implements `Readable`.

```java
    SMS message = new SMS("teacher", "Wow, this printer is able to print them, actually!");
    ArrayList<String> pages = new ArrayList<String>();
    pages.add("{3, 5} are the numbers in common between {1, 3, 5} and {2, 3, 4, 5}.");

    EBook book = new EBook("Introduction to University Mathematics.", pages);

    Printer printer = new Printer();
    printer.print(message);
    printer.print(book);
```

```output
Wow, this printer is able to print them, actually!
{3, 5} are the numbers in common between {1, 3, 5} and {2, 3, 4, 5}.
```

Let us implement another `NumberList` class, where we can add interesting readable stuff. The class has an `ArrayList` instance as object variable where we save things to read. We add items to our number list through the `add` method which receives a `Readable` variable as parameter.

```java
public class NumberList {
    private ArrayList<Readable> readables;

    public NumberList() {
        this.readables = new ArrayList<Readable>();
    }

    public void add(Readable readable) {
        this.readables.add(readable);
    }

    public int howManyReadables() {
        return this.readables.size();
    }
}
```

Number lists are usually readable, so we can implement the interface `Readable` to the class `NumberList`. The number list method `read` reads all the objects of the `readables` list, and it adds them one by one to a string which is returned by the `read()` method.

```java
public class NumberList implements Readable {
    private ArrayList<Readable> readables;

    public NumberList() {
        this.readables = new ArrayList<Readable>();
    }

    public void add(Readable readable) {
        this.readables.add(readable);
    }

    public int howManyReadables() {
        return this.readables.size();
    }

    public String read() {
        String read = "";
        for(Readable readable: this.readables) {
            read += readable.read() + "\n";
        }

        this.readables.clear();
        return read;
    }
}
```

```java
    NumberList joelList = new NumberList();
    joelList.add(new SMS("matti", "have you already written the tests?"));
    joelList.add(new SMS("matti", "did you have a look at the submissions?"));

    System.out.println("Joel has " + joelList.howManyReadables() + " messages to read");
```

```output
Joel has got 2 messages to read
```

Because the type of `NumberList` is `Readable`, we can add `NumberList` objects to our number list, too. In the example below, Joel has a lot of messages to read, luckily Mikael deals with it and reads the messages on behalf of Joel.

```java
NumberList joelList = new NumberList();
for (int i = 0; i < 1000; i++) {
    joelList.add(new SMS("matti", "have you already written the tests?"));
}

System.out.println("Joel has " + joelList.howManyReadables() + " messages to read");
System.out.println("Let's delegate some reading to Mikael");

NumberList mikaelList = new NumberList();
mikaelList.add(joelList);
mikaelList.read();

System.out.println();
System.out.println("Joel has " + joelList.howManyReadables() + " messages to read");
```

```output
Joel has 1000 messages to read
Let's delegate some reading to Mikael

Joel has 0 messages to read
```

The method `read` which is called in connection to Mikael's list parses all the `Readable` objects contained in the list, and calls their method `read`. At the end of each read method call the list is cleared. In other words, Joel's number list is cleared as soon as Mikael reads it.

*At this point, there are a lot of references; it would be good to draw down the objects and try to grasp how the `read` method call connected to `mikaelList` works!*

{% include_relative exercises/002.md %}
{: .exercises }

### An Interface as Method Return Value

As well as any other variable type, an interface can also be used as method return value. Below you find `Factory`, which can be used to produce different objects that implement the interface `Item`. In the beginning, `Factory` produces books and disks at random.

```java
public class Factory {
  public Factory(){
      // Attention: it is not necessary to write an empty constructor if there are no other constructors in the class.
      // In such cases, Java creates a default constructor, i.e a constructor without parameter
  }

   public Item produceNew(){
       Random random = new Random();
       int num = random.nextInt(4);
       if ( num==0 ) {
           return new CD("Pink Floyd", "Dark Side of the Moon", 1973);
       } else if ( num==1 ) {
           return new CD("Wigwam", "Nuclear Nightclub", 1975);
       } else if ( num==2 ) {
           return new Book("Robert Martin", "Clean Code", 1 );
       } else {
           return new Book("Kent Beck", "Test Driven Development", 0.7);
       }
   }
}
```

It is possible to use our `Factory` without knowing precisely what kind of classes are present in it, as long as they all implement Item. Below you find the class `Packer` which can be used to get a boxful of items. The `Packer` knows the factory which produces its Items:

```java
public class Packer {
   private Factory factory;

    public Packer(){
        factory = new Factory();
    }

    public Box giveABoxful() {
        Box box = new Box(100);

        for ( int i=0; i < 10; i++ ) {
            Item newItem = factory.produceNew();
            box.add(newItem);
        }

        return box;
    }
}
```

Because the packer doesn't know the classes which implement the interface `Item`, it is possble to add new classes which implement the interface without having to modify the packer. Below, we create a new class which implements our interface `Item` - `ChocolateBar`. Our Factory was modified to produce chocolate bars in addition to books and CDs. The class `Packer` works fine with the extended factory version, without having to change it.

```java
public class ChocolateBar implements Item {
    // we don't need a constructor because Java is able to generate a default one!

    public double weight(){
        return 0.2;
    }
}

public class Factory {
    // we don't need a constructor because Java is able to generate a default one!

    public Item produceNew(){
        Random random = new Random();
        int num = random.nextInt(5);
        if ( num==0 ) {
           return new CD("Pink Floyd", "Dark Side of the Moon", 1973);
        } else if ( num==1 ) {
           return new CD("Wigwam", "Nuclear Nightclub", 1975);
        } else if ( num==2 ) {
           return new Book("Robert Martin", "Clean Code", 1 );
        } else if ( num==3 ) {
           return new Book("Kent Beck", "Test Driven Development", 0.7);
        } else {
           return new ChocolateBar();
        }
    }
}
```

*Using interfaces while programming permits us to reduce the number of dependences among our classes. In our example, `Packer` is not dependent on the classes which implement interface `Item`, it is only dependent on the interface itself. This allows us to add classes wihout having to change the class `Packer`, as long as they implement our interface. We can even add classes that implement the interface to the methods which make use of our packer without compromising the process. In fact, less dependences make it **easy to extend** a program.*

### Made-Up Interfaces

Java API offers a sensible number of made-up interfaces. Below, we get to know some of Java's most used interfaces: [List](https://docs.oracle.com/javase/8/docs/api/java/util/List.html), [Map](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html), Set and [Collection](https://docs.oracle.com/javase/8/docs/api/java/util/Collection.html).

#### List

The interface `List` defines lists basic functionality. Because the class `ArrayList` implements the interface `List`, it can also be initialized through the interface `List`.

```java
List<String> strings = new ArrayList<String>();
strings.add("A String object within an ArrayList object!");
```

As we notice from the [List interface Java API](https://docs.oracle.com/javase/8/docs/api/java/util/List.html), there are a lot of classes which implement the interface `List`. A list construction which is familiar to hakers like us is the linked list. A linked list can be used through the interface `List` in the same way as the objects created from `ArrayList`.

```java
List<String> strings = new LinkedList<String>();
strings.add("A string object within a LinkedList object!");
```

Both implementations of the `List` interface work in the same way, in the user point of view. In fact, the interface *abstracts* their internal functionality. ArrayList and linkedList internal construction is evidently different, anyway. ArrayList saves the objects into a table, and the search is quick with a specific index. Differently, LinkedList builds up a list where each item has a reference to the following item. When we search for an item in a linked list, we have to go through all the list items till we reach the index.

When it comes to bigger lists, we can point out more than evident performance differences. LinkedList's strength is that adding new items is always fast. Differently, behind ArrayList there is a table which grows as it fills up. Increasing the size of the table means creating a new one and copying there the information of the old. However, searching against an index is extremely fast with an ArrayList, whereas we have to go thourgh all the list elements one by one before reaching the one we want, with a LinkedList. More information about data structures such as ArrayList and LinkedList internal implementation comes with the course Data structures and algorithms.

In our programming course you will rather want to choose ArrayList, in fact. Programming to interface is worth of it, anyway: implement your program so that you'll use data structures via interfaces.

#### Map

The Map Interface defines `HashMap` basic fuctionality. Because `HashMap`s implement the interface `Map`, it is possible to initialize them trough the interface `Map`.

```java
Map<String, String> translations = new HashMap<String, String>();
translations.put("gambatte", "tsemppiä");
translations.put("hai", "kyllä");

You get HashMap keys thourgh the method keySet.

Map<String, String> translations = new HashMap<String, String>();
translations.put("gambatte", "good luck");
translations.put("hai", "yes");

for(String key: translations.keySet()) {
    System.out.println(key + ": " + translations.get(key));
}
```

```output
gambatte: good luck
hai: yes
```

The `keySet` method returns a set made of keys which implement interface `Set` . The set which implement the interface `Set` can be parsed with a for-each loop. `HashMap` values are retrieved through the method `values`, which returns a set of values which implement the interface `Collection`. We should now focus on interfaces `Set` and `Collection`.

#### Set

The interface `Set` defines the functionality of Java's sets. Java's sets always contain 0 or 1 element of a certain type. Among the others, `HashSet` is one of the classes which implement the interface `Set`. We can parse a key set through a for-each loop, in the following way

```java
Set<String> set = new HashSet<String>();
set.add("one");
set.add("one");
set.add("two");

for (String key: set) {
    System.out.println(key);
}
```

```output
one
two
```

Notice that `HashSet` is not concerned on the order of its keys.

### Collection

The `Collection` interface defines the functionality of collections. Among the others, Java's lists and sets are collections -- that is, `List` and `Set` interfaces implement the `Collection` interface. `Collection` interface provides methods to check object existence (the contains method) and to check the collection size (size method). We can parse any class which implements the `Collection` interface with a for-each loop.

We now create a `HashMap` and parse first its keys, and then its values.

```java
Map<String, String> translations = new HashMap<String, String>();
translations.put("gambatte", "good luck");
translations.put("hai", "yes");

Set<String> keys = translations.keySet();
Collection<String> keySet = keys;

System.out.println("Keys:");
for(String key: keySet) {
    System.out.println(key);
}

System.out.println();
System.out.println("Values:");
Collection<String> values = translations.values();
for(String value: values) {
    System.out.println(value);
}
```

```output
Keys:
gambatte
hai

Values:
yes
good luck
```

The following example would have produced the same output, too.

```java
Map<String, String> translations = new HashMap<String, String>();
translations.put("gambatte", "good luck");
translations.put("hai", "yes");

System.out.println("Keys:");
for(String key: translations.keySet()) {
    System.out.println(key);
}

System.out.println();
System.out.println("Values:");
for(String value: translations.values()) {
    System.out.println(value);
}
```

In the following exercise we build an online shop, and we train to use classes through their interfaces.

{% include_relative exercises/003.md %}
{: .exercises }