---
layout: default
title: Truth values
meta: 
todo: 
---
{% include licence.md %}

## Using truth values
A variable of type truth value (`boolean`) can only have two values: either `true` or `false`). Here is an example on how to use boolean variables:

```java
int num1 = 1;
int num2 = 5;

boolean firstGreater = true;

if (num1 <= num2) {
    firstGreater = false;
}

if (firstGreater==true) {
    System.out.println("num1 is greater");
} else {
    System.out.println("num1 was not greater");
}
```

First, we assign the truth value variable `firstGreater` the value true. The first if sentence checks whether `num1` is less or equal to `num2`. If it is, we change the value of firstGreater to *false*. The later if sentence selects which string to print based on the truth value.

As a matter of fact, using a truth value in a conditional sentence is easier than the description in the previous example. We can write the second if sentence as follows:

```java
if (firstGreater) {  // means the same as firstGreater==true
    System.out.println("num1 was greater");
} else {
    System.out.println("num1 was not greater");
}
```

If we want to check if the boolean variable holds the value true, we do not need to write `==true`, just writing the name of the variable is enough!

If we want to check if the boolean variable holds the value false, we can check that using the negation operation ! (exclamation mark):

```java
if (!firstGreater) {  // means the same as firstGreater==false
    System.out.println("num1 was not greater");
} else {
    System.out.println("num1 was greater");
}
```

### Methods that return a truth value

Truth values come in especially handy when we want to write methods that check for validity. Let us create a method that checks if the list it gets as a parameter includes only positive numbers (here 0 is considered positive). The method returns the information as a boolean (i.e. truth value).

```java
public static boolean allPositive(ArrayList<Integer> numbers) {
    boolean noNegative = true;

    for (int number : numbers) {
        if (number < 0) {
            noNegative = false;
        }
    }

    // if one of the numbers on the list had a value that is below zero, noNegatives becomes false.

    return noNegative;
}
```

The method has a boolean helper variable called `noNegative`. First we assign the helper variable the value true. The method checks all numbers on the list one by one. If at least one number is less than 0, we assign the helper variable the value false. In the end the method returns the value of the helper variable. If no negative numbers were found, it has the value true, otherwise it has the value false.

The method is used as follows:

```java
public static void main(String[] args) {

    ArrayList<Integer> numbers = new ArrayList<Integer>();
    numbers.add(3);
    numbers.add(1);
    numbers.add(-1);

    boolean result = allPositive(numbers);

    if (result) {  // means the same as result == true
        System.out.println("all numbers are positive");
    } else {
        System.out.println("there is at least one negative number");
    }
}
```

Usually it is not necessary to store the answer into a variable. We can write the method call directly as the condition:

```java
ArrayList<Integer> numbers = new ArrayList<Integer>();
numbers.add(4);
numbers.add(7);
numbers.add(12);
numbers.add(9);

if (allPositive(numbers)) {
    System.out.println("all numbers are positive");
} else {
    System.out.println("there is at least one negative number");
}
```

### The return command and ending a method

The execution of a method is stopped immediately when a command called `return` is executed. Using this information to our advantage, we write the `allPositive` method easier to understand.

```java
public static boolean allPositive(ArrayList<Integer> numbers) {
    for (int number : numbers) {
        if (number < 0) {
            return false;
        }
    }

    // if the execution reached this far, no negative numbers were found
    // so we return true
    return true;
}
```

When we are going through the list of numbers and we find a negative number, we can exit the method by returning false. If there are no negative numbers on the list, we get to the end and therefore can return the value true. We now got rid of the helper variable inside the method!

{% include_relative exercises/001.md %}
{% include_relative exercises/002.md %}
{: .exercises }