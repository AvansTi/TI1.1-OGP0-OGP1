---
layout: default
title: Sorting
meta: Put extra info here, like if there any subjects required for this subject
todo: what should be improved in this chapter
---
{% include licence.md %}

## Sorting an array

We'll get back to arrays again.

### Sorting an array with the ready-made tools of Java.

As we've seen, there's all kinds of useful things already in Java. For example for handling ArrayLists you can find many useful help methods in the class Collections. For arrays you can find helpful methods in the class `Arrays`. Sorting a table can be done with `Arrays.sort(array)`.

**Note**: To be able to use the command you must have the following definition at the top of the program file:

```java
import java.util.Arrays;
```

*If you forget to write the `import` line, IntelliJ will offer help with writing it. Try clicking the picture of the "bulp" that appears to the left from the line of code that is underlined with red*.

The following program creates arrays and sorts the values in the array with the `Arrays.sort`-command.

```java
int[] values = {-3, -111, 7, 42};
Arrays.sort(values);
for(int value: values) {
    System.out.println(value);
}
```

```output
-111
-3
7
42
```

### Implementation of a sorting algorithm

It's easy to sort an array with the ready-made tools of Java. The general knowledge of a program requires knowing at least one sorting algorithm (or in other words, a way to sort an array). Let's get familiar with the "classic" sorting algorithm, choice sorting. Let's do this with a few excercise.

{% include_relative exercises/001.md %}
{: .exercises }
