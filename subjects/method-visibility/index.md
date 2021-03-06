---
layout: default
title: Method visibility
meta: 
todo: 
---
{% include licence.md %}

## More about methods

### Methods and visibility of variables

Let us try to change from within a method the value of a variable located in the main program.

```java
// main program
public static void main(String[] args) {
    int number = 1;
    addThree();
}

// method
public static void addThree() {
    number = number + 3;
}
```

Unfortunately this program will not work, because the method cannot "see" the variable `number` located in the main program.

This holds generally. Variables defined in the main program are not visible for other methods. Also, the other way is similar: variables defined in methods are not visible for other methods or the main program. The only way to give information to a method from the outside is to use parameters.

```java
// main program
public static void main(String[] args) {
    int number = 1;
    System.out.println("Main program variable number holds the value: " + number);
    addThree(number);
    System.out.println("Main program variable number holds the value: " + number);
}

// method
public static void addThree(int number) {
    System.out.println("Method parameter number holds the value: " + number);
    number = number + 3;
    System.out.println("Method parameter number holds the value: " + number);
}
```
{: .interactive #method-visibility-1 }

In the program above the method addThree has a parameter called `number`. This parameter is copied (duplicated) for the method to use. When the program above is executed we see the following output:

The number we gave as a parameter to the method was *copied* for the method to use. If we would like the main program to be able to use the new value generated by the method, the method needs to return that value.

