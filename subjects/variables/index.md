---
layout: default
title: Compiler, Setup and Printing
meta: Put extra info here, like if there any subjects required for this subject
---
{% include licence.md %}

## Variables and assignment

### Variables and data types

A *variable* is one of the most important concepts in computer programming. A variable should be imagined as a box in which you can store information. The information stored in a variable always has a type. Java only has a limited number of data types, but it can be extended with custom types. Those custom types can be recognized, as their name is always spelled with a capital. The basic set of variable types in java is as followed:

| Type      | Memory size   | Range  | Default | Description |
|-----------|---------------|--------|---------|-------------|
| byte      | 1 byte        | -$$128$$ to $$127$$                                                         | 0       | The smallest numeric datatype in java. Can be used for large collections of data to save memory. |
| short     | 2 bytes       | $$-32 768$$ to $$32 767$$                                                   | 0       | A small numeric datatype in java. Can be used for large collections of data to save memory |
| int       | 4 bytes       | $$-2^{31}$$ to $$2^{31} - 1$$                                       | 0       | The default datatype for numbers. This number is 32bit and processors are optimized to handle these numbers |
| long      | 8 bytes       | $$-2^{63}$$ to $$2^{63} - 1$$                                       | 0L      | Used when the int datatype is not big enough |
| float     | 4 bytes       | $$-(2-2^{-23}) \times 2^{127}$$ to $$(2-2^{-23}) \times 2^{127}$$   | 0.0f    | The floating point type is used for storing non-integer values. This is not a precise datatype, and should not be used for currency where precision is required
| double    | 8 bytes       | $$-(2-2^{-52}) \times 2^{1023}$$ to $$(2-2^{-52}) \times 2^{1023}$$ | 0.0d    | The double is used for storing non-integer values. This is not a precise datatype, and should not be used for currency where precision is required. A double has more memory space than a float, which is used for storing numbers with more precision | 
| boolean   | not defined   | true, false                                                         | false   | Used for simple truth values of true or false. Are used becaused they are easy to used in expressions | 
| char      | 2 bytes       | all unicode characters                                              | '\u0000'| Used for storing the characters in a text. Can contain values like 'a', 'Z', '0' or '@' |

Another type that you have seen so far is the `String`. A string is a variable that contain text

A value can be assigned to a variable using the equals sign (=).

```java
int months = 12;
```

In the statement above, we assign the value 12 to the variable named `months` whose data type is integer (int). The statement is read as "the variable months is assigned the *value* 12".

The value of the variable can be appended to a string with the plus + sign as shown in the following example.

```java
String text = "includes text";
int wholeNumber = 123;
double decimalNumber = 3.141592653;
boolean isTrue = true;

System.out.println("The variable's type is text. Its value is " + text);
System.out.println("The variable's type is integer. Its value is  " + wholeNumber);
System.out.println("The variable's type is decimal number. Its value is " + decimalNumber);
System.out.println("The variable's type is truth value. Its value is " + isTrue);
```
Printing:
```output
The variable's type is String. Its value is includes text
The variable's type is int. Its value is 123
The variable's type is double. Its value is 3.141592653
The variable's type is boolean. Its value is true
```

A variable holds its value until it is assigned a new one. Note that the variable type is written only when the variable is first declared in the program. After that we can use the variable by its name.

```java
int wholeNumber = 123;
System.out.println("The variable's type is integer. Its value is  " + wholeNumber);

wholeNumber = 42;
System.out.println("The variable's type is integer. Its value is  " + wholeNumber);
```

The output is:

```output
The variable's type is integer. Its value is 123
The variable's type is integer. Its value is 42
```

### Variable data types are immutable

When a variable is declared with a data type, it cannot be changed later. For example, a text variable cannot be changed into an integer variable and it cannot be assigned integer values.

```java
String text = "yabbadabbadoo!";
text = 42; // Does not work! :(
```

Integer values can be assigned to decimal number variables, because whole numbers are also decimal numbers.

```java
double decimalNumber = 0.42;
decimalNumber = 1; // Works! :)
```

{% include_relative exercises/001.md %}
{: .exercises }

### Allowed and descriptive variable names

There are certain limitations on the naming of our variables. Even though umlauts, for example, can be used, it is better to avoid them, because problems might arise with [character encoding](http://en.wikipedia.org/wiki/Character_encoding). For example, it is recommended to use A instead of Ä.

Variable names must not contain certain special characters like exclamation marks (!). Space characters cannot be used, either, as it is used to separate commands into multiple parts. It is a good idea to replace the space character using a [camelCase](https://en.wikipedia.org/wiki/Camel_case) notation. **Note**: The first character is always written in lower case when using the camel case notation.

```java
int camelCaseVariable = 7;
```

Variable names can contain numbers as long it does not start with one. Variable names cannot be composed solely of numbers, either.

```java
int 7variable = 4; // Not allowed!
int variable7 = 4; // A valid, but not descriptive variable name
```

Variable names that have been defined before cannot be used. Command names such as `System.out.print` cannot be used, either.

```java
int camelCase = 2;
int camelCase = 5; // Not allowed, the variable camelCase is already defined!
```

It is strongly recommended to name variables so that their purpose can be understood without comments and without thinking. Variable names used in this course **must** be descriptive.

#### Valid variable names

* lastDay = 20
* firstYear = 1952
* name = "Matti"

#### Invalid variable names

* last day of the month = 20
* 1day = 1952
* watchout! = 1910
* 1920 = 1

## Calculation

The calculation operations are pretty straightforward: +, -, * and /. A more peculiar operation is the modulo operation %, which calculates the remainder of a division. The order of operations is also pretty straightforward: the operations are calculated from left to right taking the parentheses into account.

```java
int first = 2;   // variable of whole number type is assigned the value 2
int second = 4;  // variable of whole number type is assigned the value 4
int sum = first + second;  // variable of whole number type is assigned the value of first + second
                           //     (which means 2 + 4)

System.out.println(sum); // the value of the sum of variables is printed
```

```java
int calcWithParens = (1 + 1) + 3 * (2 + 5);  // 23
int calcWithoutParens = 1 + 1 + 3 * 2 + 5;   // 13
```

The parentheses example above can also be done step by step.

```java
int calcWithParens = (1 + 1);
calcWithParens = calcWithParens + 3 * (2 + 5);  // 23

int calcWithoutParens = 1 + 1;
calcWithoutParens = calcWithoutParens + 3 * 2;
calcWithoutParens = calcWithoutParens + 5;      // 13
```
{: .interactive .hideStack .hideOutput #variables-calc }

Calculation operations can be used almost anywhere in the program code.

```java
int first = 2;
int second = 4;

System.out.println(first + second);
System.out.println(2 + second - first - second);
```

### Floating point numbers (decimal numbers)

Calculating the division and remainder of whole numbers is a little trickier. A floating point number (decimal number) and integer (whole number) often get mixed up. If all the variables in a calculation operation are integers, the end result will also be an integer.

```java
int result = 3 / 2;  // result is 1 (integer) because 3 and 2 are integers as well
```

```java
int first = 3:
int second = 2;
double result = first / second;  // the result is again 1 because first and second are integers
```

The remainder can be calculated using the remainder operation (%). For example, the calculation 7 % 2 yields 1.

```java
int remainder = 7 % 2;  // remainder is 1 (integer)
```

If either the dividend or the divisor (or both!) is a floating point number (decimal number) the end result will also be a floating point number.

```java
double whenDividendIsFloat = 3.0 / 2;  // result is: 1.5
double whenDivisorIsFloat = 3 / 2.0;   // result is: 1.5
```

If needed, integers can be converted to floating point using the type cast operation `(double)` as follows

```java
int first = 3;
int second = 2;
double result1 = (double)first / second;  // result is: 1.5

double result2 = first / (double)second;  // result is: 1.5

double result3 = (double)(first / second);  // result is: 1
```

In the last example calculation, the result is rounded incorrectly because the calculation between the integers is done before the type cast to a floating point number.

If the quotient is assigned to a variable of integer type, the result will be an integer as well.

```java
int integerResultBecauseTypeIsInteger = 3.0 / 2;  // quotient is automatically integer: 1
```

The next example will print "1.5" because the dividend is transformed into a floating point number by multiplying it with a floating point number (1.0 * 3 = 3.0) before the division.

```java
int dividend = 3;
int divisor = 2;

double quotient = 1.0 * dividend / divisor;
System.out.println(quotient);
```

What does the following code print?

```java
int dividend = 3;
int divisor = 2;

double quotient = dividend / divisor * 1.0;
System.out.println(quotient);
```

From now on, make sure that you name your variables that follow good conventions like the variables in the examples above.

{% include_relative exercises/002.md %}
{: .exercises }

## Concatenation or combining strings

Let us take a closer look on combining strings with the + operator.

If the + operator is used between two strings, a new string is created with the two strings combined. Note the clever use of space characters in the values of the variables below!

```java
String greeting = "Hi ";
String name = "John";
String goodbye = ", and goodbye!";

String sentence = greeting + name + goodbye;

System.out.println(sentence);
```
{: .interactive .hideStack #variables-concat }

```output
Hi John, and goodbye!
```

If a string is on either side of the + operator, the other side is converted to a string and a new string is created. For example, the integer 2 will be converted into the string "2" and then combined with the other string.


```java
System.out.println("there is an integer --> " + 2);
System.out.println(2 + " <-- there is an integer");
```

What we learned earlier about the order of operations is still valid:

```java
System.out.println("Four: " + (2 + 2));
System.out.println("But! Twenty-two: " + 2 + 2);
```

```output
Four: 4
But! Twenty-two: 22
```

Using this information, we can print a mix of strings and values of variables:

```java
int x = 10;

System.out.println("variable x has the following value: " + x);

int y = 5;
int z = 6;

System.out.println("y has the value  " + y + " and z has the value " + z);
```

This program obviously prints:

```output
variable x has the following value: 10
y has the value 5 and z has the value 6
```

{% include_relative exercises/003.md %}
{% include_relative exercises/004.md %}
{: .exercises }
