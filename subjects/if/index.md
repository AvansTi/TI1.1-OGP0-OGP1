---
layout: default
title: If statement
meta: Put extra info here, like if there any subjects required for this subject
---
{% include licence.md %}

## Conditional statements and truth values

So far, our programs have progressed from one command to another in a straightforward manner. In order for the program to *branch* to different execution paths based on e.g. user input, we need conditional statements.

```java
int number = 11;

if (number > 10) {
    System.out.println("The number was greater than 10");
}
```

The condition `(number > 10)` evaluates into a truth value; either `true` or `false`. The if command only handles truth values. The conditional statement above is read as "if the number is greater than 10".

Note that the `if` statement is not followed by semicolon as the condition path continues after the statement.

After the condition, the opening curly brace `{` starts a new *block*, which is executed if the condition is true. The *block* ends with a closing curly brace `}`. Blocks can be as long as desired.

The comparison operators are:

* \> Greater than
* \>= Greater than or equal to
* < Less than
* <= Less than or equal to
* == Equals
* != Not equal

```java
int number = 55;

if (number != 0) {
    System.out.println("The number was not equal to 0");
}

if (number >= 1000) {
    System.out.println("The number was greater than or equal to 1000");
}
```
{: .interactive .hideStack #if-1 }

A block can contain any code including other `if` statements.

```java
int x = 45;
int number = 55;

if (number > 0) {
    System.out.println("The number is positive!");
    if (number > x) {
        System.out.println(" and greater than the value of variable x");
        System.out.println("after all, the value of variable x is " + x);
    }
}
```
{: .interactive .hideStack #if-2 }

The comparison operators can also be used outside the if statements. In such case the truth value will be stored in a truth value variable.

```java
int first = 1;
int second = 3;

boolean isGreater = first > second;
```

In the example above the boolean (i.e. a truth value) variable `isGreater` now includes the truth value `false`.

A boolean variable can be used as a condition in a conditional sentence.

```java
int first = 1;
int second = 3;

boolean isLesser = first < second;

if (isLesser) {
    System.out.println(first + " is less than " + second + "!");
}
```

```output
1 is less than 3!
```

### else if

If there are more than two conditions for the program to check, it is recommended to use the `else if` command. It works like the `else` command, but with an additional condition. `else if` comes after the `if` command. There can be multiple `else if` commands.

```java
int number = 3;

if (number == 1) {
    System.out.println("The number is one.");
} else if (number == 2) {
    System.out.println("The number is two.");
} else if (number == 3) {
    System.out.println("The number is three!");
} else {
    System.out.println("Quite a lot!");
}
```
{: .interactive .hideStack #if-3 }

Let us read out loud the example above: If number is one, print out "The number is one.". Otherwise if the number is two, print out "The number is two.". Otherwise if the number is three, print out "The number is three!". Otherwise print out "Quite a lot!".

### Comparing strings

Strings cannot be compared using the equality operator (==). For string comparison, we use the `equals`. command, which is always associated with the string to compare.

```java
String text = "course";

if (text.equals("marzipan")) {
    System.out.println("The variable text contains the text marzipan");
} else {
    System.out.println("The variable text does not contain the text marzipan");
}
```
{: .interactive .hideStack #if-4 }

The `equals` command is always attached to the string variable with a dot in between. A string variable can also be compared to another string variable.

```java
String text = "course";
String anotherText = "horse";

if (text.equals(anotherText)) {
    System.out.println("The texts are the same!");
} else {
    System.out.println("The texts are not the same!");
}
```
{: .interactive .hideStack #if-5 }

When comparing strings, it is crucial to make sure that both string variables have been assigned some value. If a value has not been assigned, the program execution terminates with a *NullPointerException* error, which means that variable has no value assigned to it (null).

{% include_relative exercises/001.md %}
{% include_relative exercises/002.md %}
{: .exercises }

### Logical operations

The condition statements can be made more complicated using logical operations. The logical operations are:

* `condition1 && condition2` is true if both conditions are true.
* `condition1 || condition2` is true if either of the conditions are true.
* `!condition` is true if the condition is false.

Below we will use the AND operation && to combine two individual conditions in order to check if the value of the variable is greater than 4 *and* less than 11 (i.e. in the range 5 - 10).

```java
System.out.println("Is the number between 5-10?");
int number = 7;

if (number > 4 && number < 11) {
    System.out.println("Yes! :)");
} else {
    System.out.println("Nope :(")
}
```

```output
Is the number between 5-10?
Yes! :)
```

Next up is the OR operation ||, which will be used to check if the value is less than 0 or greater than 100. The condition evaluates to true if the value fulfills either condition.

```java
System.out.println("Is the number less than 0 or greater than 100?");
int number = 145;

if (number < 0 || number > 100) {
    System.out.println("Yes! :)");
} else {
    System.out.println("Nope :(")
}
```

```output
Is the number less than 0 or greater than 100?
Yes! :)
```

Now we will use the negation operation ! to negate the condition:

```java
System.out.println("Is the string equal to 'milk'?");
String text = "water";

if (!(text.equals("milk"))) {  // true if the condition text.equals("milk") is false
    System.out.println("No!");
} else {
    System.out.println("Yes")
}
```

```output
Is the text equal to 'milk'?
No!
```

For complicated conditions, we often need parentheses:

```java
int number = 99;

if ((number > 0 && number < 10) || number > 100 ) {
    System.out.println("The number was in the range 1-9 or it was over 100");
} else {
    System.out.println("The number was equal to or less than 0 or it was in the range 10-99");
}
```

```output
The number was equal to or less than 0 or it was in the range 10-99
```

{% include_relative exercises/003.md %}
{% include_relative exercises/004.md %}
{% include_relative exercises/005.md %}
{: .exercises }

## Changing variables

We usually want to change the value of an existing variable. This can be done using the normal assignment statement. In the next example, we increase the value of the variable `age` by one:

```java
int age = 1;

System.out.println(age);  // prints 1
age = age + 1;            // the new value of age is the old value of age + 1
System.out.println(age);  // prints 2
```
{: .interactive .hideStack #if-6 }

The `age = age + 1` statement increments the value of the variable `age` by one. It is also possible to increment a variable by one as below:

```java
int age = 1;

System.out.println(age);  // prints 1
age++;                    // means the same as age = age + 1
System.out.println(age);  // prints 2
```
{: .interactive .hideStack #if-7 }

Another example:

```java
int length = 100;

System.out.println(length);  // prints 100
length = length - 50;
System.out.println(length);  // prints 50
length = length * 2;
System.out.println(length);  // prints 100
length = length / 4;
System.out.println(length);  // prints 25
length--;                    // means the same as length = length - 1;
System.out.println(length);  // prints 24
```
{: .interactive .hideStack #if-8 }

### else

If the truth value of the comparison is false, another optional block can be executed using the `else` command.

```java
int number = 4;

if (number > 5) {
    System.out.println("Your number is greater than five!");
} else {
    System.out.println("Your number is equal to or less than five!");
}
```
{: .interactive .hideStack #if-9 }

{% include_relative exercises/006.md %}
{: .exercises }