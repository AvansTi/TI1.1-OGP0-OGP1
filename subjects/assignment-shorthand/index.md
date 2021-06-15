---
layout: default
title: Shorthand assignment notation
meta: 
todo: 
---
{% include licence.md %}

## Assignment operations

Because changing the value of a variable is a very common operation, Java has special assignment operations for it.

```java
int length = 100;

length += 10;  // same as length = length + 10;
length -= 50;  // same as length = length - 50;
```
{: .interactive .hideStack #assignments-shorthand-1 }


When performing the assignment operation on an existing variable, it is written as `variable operation= change`, for example `variable += 5`. Note that a variable must be defined before you can assign a value to it. Defining a variable is done by specifying the variable type and the name of the variable.

The following example will not work because the type of the variable `length` has not been defined.

```java
length = length + 100;  // error!
length += 100;          // error!
```

When the type is defined, the operations will also work.

```java
int length = 0;
length = length + 100;
length += 100;

// the variable length now holds the value 200
```
{: .interactive .hideStack #assignments-shorthand-2 }

There are also other assignment operations:

```java
int length = 100;

length *= 10;   // same as length = length * 10;
length /= 100;  // same as length = length / 100;
length %= 3;    // same as length = length % 3;

// the variable length now holds the value 1
```
{: .interactive .hideStack #assignments-shorthand-3 }

Often during a loop, the value of a variable is calculated based on repetition. The following program calculates 3*4 somewhat clumsily as the sum 3+3+3+3:

```java
int result = 0;

int i = 0;
while (i < 4) {
   result = result + 3;
   i++;  // means the same as i = i + 1;
}
```
{: .interactive .hideStack #assignments-shorthand-4 }


In the beginning `result = 0`. During the loop, the value of the variable is incremented by 3 on each iteration. Because there are 4 iterations, the value of the variable is 3*4 in the end.

Using the assignment operator introduced above, we can achieve the same behavior as follows:

```java
int result = 0;

int i = 0;
while (i < 4) {
   result += 3;  // this is the same as result = result + 3;
   i++;          // means the same as i = i+1;
}
```
{: .interactive .hideStack #assignments-shorthand-5 }


{% include_relative exercises/001.md %}
{% include_relative exercises/002.md %}
{% include_relative exercises/003.md %}
{% include_relative exercises/004.md %}
{: .exercises }
