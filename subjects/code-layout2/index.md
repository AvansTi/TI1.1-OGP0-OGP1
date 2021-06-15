---
layout: default
title: Instructions on code-writing and problem solving
meta: Put extra info here, like if there any subjects required for this subject
todo: what should be improved in this chapter
---
{% include licence.md %}

## Instructions on code-writing and problem solving

Two of the leading software developers, *Martin Fowler* and *Kent Beck* have said in the book *Refactoring: Improving the Design of Existing Code* that:

* Fowler: *"Any fool can write code that a computer can understand. Good programmers write code that humans can understand."*
* Beck: *"I'm not a great programmer, I'm just good a programmer with great habits."*

[Update: previously both quotes were credited to Kent Beck. Our thanks go to Esko Luontola for [pointing out this mistake](http://sourceforge.net/p/mooc-issues/tickets/451/)]:

We are now taking the first steps towards becoming good programmers.

### Well indented and "breathing" code

Let us take a look at a code that first adds numbers to a list and then prints the items fo the list. Then all instances of a certain number are removed from the list and the list gets printed.

First, we write the code badly and without indentations:

```java
public static void main(String[] args) {
ArrayList<Integer> numbers = new ArrayList<Integer>();
numbers.add(4);
numbers.add(3);
numbers.add(7);
numbers.add(3);
System.out.println("The numbers in the beginning:");
for (int number : numbers) {
System.out.println(number);
}
while (numbers.contains(Integer.valueOf(3))) {
numbers.remove(Integer.valueOf(3));
}
System.out.println("The numbers after removal:");
for (int number : numbers) {
System.out.println(number);
}
```

Even though the unindented code works, it is unpleasant to read. Let us indent the code (you can get IntelliJ to auto-indent your code by pressing Alt+F8) and separate logical parts with line breaks:

```java
public static void main(String[] args) {
    ArrayList<Integer> numbers = new ArrayList<Integer>();
    numbers.add(4);
    numbers.add(3);
    numbers.add(7);
    numbers.add(3);

    System.out.println("The numbers in the beginning:");

    // here we print numbers
    for (int number : numbers) {
        System.out.println(number);
    }

    // checks if the list contains the number 3
    while (numbers.contains(Integer.valueOf(3))) {
        numbers.remove(Integer.valueOf(3));  // if yes, it is removed
    }
    // we use a while structure to get all the threes removed!

    System.out.println("The numbers after removal:");

     // here we print numbers
    for (int number : numbers) {
        System.out.println(number);
    }
}
```

Now, the code starts to make sense. For example, the printing and the number removal are two logical parts, therefore they are separated with line breaks. The code is *airy* and reading the code is much more pleasant.

There are even comments in the code to help the reader understand what happens and where!

### Getting rid of copy-paste with methods

What could be called the Original sin of a programmer is to create copy-paste code. This means using the same code in multiple places by copy-pasting it around the source code. In our example, the printing of the list is done twice. The code that handles the printing part should be separated as its own method. Then the printing method should be called from the main program:

```java
public static void main(String[] args) {
    ArrayList<Integer> numbers = new ArrayList<Integer>();
    numbers.add(4);
    numbers.add(3);
    numbers.add(7);
    numbers.add(3);

    System.out.println("The numbers in the beginning:");

    // here we print numbers
    print(numbers);

    while (numbers.contains(Integer.valueOf(3))) {
        numbers.remove(Integer.valueOf(3));
    }

    System.out.println("The numbers after removal:");

    // here we print numbers
    print(numbers);
}

public static void print(ArrayList<Integer> numbers) {
    for (int number : numbers) {
        System.out.println( number );
    }
}
```

### Slicing separate tasks into methods with descriptive names

Now, the code has become even more easy to read. A distinctively separate entity, the printing of the list is now a method that is easy to understand. By defining a new method the readability of the main program has improved. Pay attention to the descriptive name of the method: the name describes exactly what the method does. Next, we can remove the advising comments here we *print numbers*, because the name of the method speaks for itself.

There is still room for improvements in writing the program. The main program still looks a bit messy, since there is an "unaesthetic" code line that directly manipulates the list, in between the neat method calls. Let us turn that unaesthetic piece of code into a method:

```java
public static void main(String[] args) {
    ArrayList<Integer> numbers = new ArrayList<Integer>();
    numbers.add(4);
    numbers.add(3);
    numbers.add(7);
    numbers.add(3);

    System.out.println("The numbers in the beginning:");
    print(numbers);

    remove(numbers, 3);

    System.out.println("The numbers after removal:");
    print(numbers);
}

public static void print(ArrayList<Integer> numbers) {
    for (int number : numbers) {
        System.out.println( number );
    }
}

public static void remove(ArrayList<Integer> numbers, int removed) {
    while (numbers.contains(Integer.valueOf(removed))) {
        numbers.remove(Integer.valueOf(removed));
    }
}
```

In the example above, we created a new descriptively named method out of a separate logical entity, i.e. removing all the instances of a certain number. The resulting main program is now very understandable - almost like natural language. Both methods are very simple and easy to understand as well.

Kent Beck might be proud of what we have accomplished! The code is easy to understand, easy to modify and does not include any copy-paste.