---
layout: default
title: Nesting
meta: Put extra info here, like if there any subjects required for this subject
todo: what should be improved in this chapter
---
{% include licence.md %}

## About blocks and nested loops

A piece of code that begins with a curly bracket { and ends with a curly bracket } is called a block. As we've already seen, blocks are used - among other things - to denote the code of conditional and loop sentences. An important feature of a block is that variables defined within it only exist within it..

In the following example we define the string variable stringDefinedWithinBlock within the block of a conditional sentence, which therefor will only exist within the block. The variable introduced within the block cannot be printed outside of it!

```java
int number = 5;

if( number == 5 ){
    String stringDefinedWithinBlock = "Yeah!";
}

System.out.println(stringDefinedWithinBlock); // does not work!
```

However, you can use and manipulate variables defined outside of the block in the block.

```java
int number = 5;

if( number == 5 ) {
    number = 6;
}

System.out.println(number); // prints 6
```

You can have any kind of code within a block. For example, a for loop can have another for loop within it or say, a while loop. Let's inspect the following program:

```java
for(int i = 0; i < 3; i++) {
   System.out.print(i + ": ");

   for(int j = 0; j < 3; j++) {
      System.out.print(j + " ");
   }

   System.out.println();
}
```

The program prints the following:

```output
0: 0 1 2
1: 0 1 2
2: 0 1 2
```

So what happens in the program? If we only think about the outer for loop, its functionality is easy to understand:

```java
for(int i = 0; i < 3; i++) {
   System.out.print(i + ": ");

   // the inner for-loop

   System.out.println();
}
```

So first i=0 prints 0: and a carriage return. After this i grows and 1 is printed and so forth, so the outer for makes this happen:

```output
0:
1:
2:
```

The inner for loop is also easy to understand separately. It prints out `0 1 2`. When we combine these two, we'll notice that the inner for loop carries out its print just before the outer for loop's carriage return.

### variables defined outside of a for loop as its condition

Let's inspect the following alteration to the previous example:

```java
for(int i = 0; i < 3; i++) {
    System.out.print(i + ": ");

    for(int j = 0; j <= i; j++) {
        System.out.print(j + " ");
    }

    System.out.println();
}
```

The amount of runs the inner for loop does now depends on the value of the variable i of the outer loop. So when i=0 the inner loop prints 0, when `i=1` the inner loop prints 0 1. The entire output of the program is as follows:

```output
0: 0
1: 0 1
2: 0 1 2
```

The following program prints out the multiplication tables of the numbers 1 .. 10.

```java
for(int i = 1; i <= 10; i++) {

    for(int j = 1; j <= 10; j++) {
        System.out.print(i * j + " ");
    }

    System.out.println();
}
```

The output looks like this:

```output
1 2 3 4 5 6 7 8 9 10
2 4 6 8 10 12 14 16 18 20
3 6 9 12 15 18 21 24 27 30
4 8 12 16 20 24 28 32 36 40
5 10 15 20 25 30 35 40 45 50
6 12 18 24 30 36 42 48 54 60
7 14 21 28 35 42 49 56 63 70
8 16 24 32 40 48 56 64 72 80
9 18 27 36 45 54 63 72 81 90
10 20 30 40 50 60 70 80 90 100
```

The topmost row has the multiplication table of 1. At the beginning `i=1` and the inner loop's variable `j` gets the values 1...10. For each `i`, `j` value pair their product is printed. So at the beginning `i=1`, `j=1`, then `i=1`, `j=2`, ..., `i=1`, `j=10` next `i=2`, `j=1`, and so forth.

Of course the multiplication table program can be cut in to smaller pieces, too. We can define the methods `public void printMultiplicationTableRow(int multiplier, int howManyTimes)` and `public void printMultiplicationTable(int upTo)`, in this case the structure of our program could be as follows:

```java
public class MultiplicationTable {

    public void print(int upTo) {
        for(int i = 1; i <= upTo; i++) {
            printMultiplicationTableRow(i, upTo);

            System.out.println();
        }
    }

    public void printMultiplicationTableRow(int multiplier, int howManyTimes) {
        for(int i = 1; j <= howManyTimes; i++) {
            System.out.print(i * multiplier + " ");
        }
    }
}
```

Now calling `new MultiplicationTable().print(5)`; prints the tables below.

```output
1 2 3 4 5
2 4 6 8 10
3 6 9 12 15
4 8 12 16 20
5 10 15 20 25
```

{% include_relative exercises/001.md %}
{% include_relative exercises/002.md %}
{: .exercises }
