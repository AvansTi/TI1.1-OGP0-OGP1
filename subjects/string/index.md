---
layout: default
title: Strings
meta: 
todo: 
---
{% include licence.md %}

## Strings of characters

In this section, we take a closer look at strings of characters in Java, which are called `Strings`. We have already used variables of String type when printing, and learned how to compare Strings. Comparing two strings is performed by calling the equals() method of the string.


```java
String animal = "Dog";

if( animal.equals("Dog") ) {
    System.out.println(animal + " says bow-wow");
} else if ( animal.equals("Cat") ) {
    System.out.println(cat + " says meow meow");
}
```

It is possible to ask the string how many characters long it is by writing `.length()` after it's name. In other words, we are calling its length() method.

```java
String banana = "banana";
String cucumber = "cucumber";
String together = banana + cucumber;

System.out.println("The length of banana is " + banana.length());
System.out.println("The length of  cucumber is " + cucumber.length());
System.out.println("The word " + together + " length is " + together.length());
```

In the above code, the method `length()` is called for three different strings. The call `banana.length()` calls only the method that gives the length of the string banana, while `cucumber.length()` calls the method that gives the length of the string cucumber etc. The left part before the dot says whose method is called.

Java has a special data type, called `char`, to be used for characters. A `char` variable can store only one character. A string variable can return a character from a specific location in itself with the method `charAt()` that uses the index of the location as a parameter. Note that counting the index of the character starts from zero!

```java
String word = "Supercalifragilisticexpialidocious";

char character = word.charAt(3);
System.out.println("The 4th character of the word is " + character); //prints "e"
```

The characters in a string are numbered (indexed) starting from 0. This means that we can reach the last character in a string with number (or index) "the length of the word minus one", or `word.charAt(word.length()-1)`. The following example will make the program crash, because we are trying to get a character from an index that does not exist.

```java
char character = word.charAt(word.length());
```

{% include_relative exercises/001.md %}
{% include_relative exercises/002.md %}
{% include_relative exercises/003.md %}
{% include_relative exercises/004.md %}
{% include_relative exercises/005.md %}
{% include_relative exercises/006.md %}
{: .exercises }

### Other methods for strings

We often want to read only a specific part of a string. A method in the String class called `substring` makes this possible. It can be used in two ways:

```java
String word = "Supercalifragilisticexpialidocious";
System.out.println(word.substring(14)); //prints "listicexpialidocious"
System.out.println(word.substring(9,20)); //prints "fragilistic"
```

We can store the return value in a variable, because the return value of the substring method is of type String.

```java
String book = "Mary Poppins";
String endpart = book.substring(5);
System.out.println("Harry " + endpart); // prints "Harry Poppins"
```

Methods in the String class also make it possible to search for a specific word in text. For example, the word "or" can be found in the word "Horse". A method called `indexOf()` searches for the word given as a parameter in a string. If the word is found, it returns the starting index (location), remember that the numbering starts from 0 of the word. If the word is not found, the method returns the value -1.

```java
String word = "aesthetically";

int index = word.indexOf("tic"); // index value will be 6
System.out.println(word.substring(index)); //prints "tically"

index = word.indexOf("ally"); //index value will be 9
System.out.println(word.substring(index)); //prints "ally"

index = word.indexOf("book"); // string "aesthetically" does not include "book"
System.out.println(index); //prints -1
System.out.println(word.substring(index)); //error!
```

{% include_relative exercises/007.md %}
{% include_relative exercises/008.md %}
{% include_relative exercises/009.md %}
{% include_relative exercises/010.md %}
{: .exercises }