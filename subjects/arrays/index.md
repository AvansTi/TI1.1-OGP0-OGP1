---
layout: default
title: Arrays
meta: Put extra info here, like if there any subjects required for this subject
todo: what should be improved in this chapter
---
{% include licence.md %}

## Array

During the course, we've used ArrayLists numerous times to store different kinds of objects. ArrayList is easy to use because it offers a lot of ready-made tools that make the programmer's life a little easier: automatic growing of a list, thanks to the list which doesn't run out of space (unless of course the list grows so large that it makes the program take up all the memory that is reserved for it), for example.

Array is an object that can be understood as a series of pigeonholes for values. The length or size of an array is the number of spots in that array - the number of items you can put in the array. The values of an array are called cells of the array. Unlike with ArrayLists, the size of the array (the amount of cells in an array) cannot be changed, growing an array always requires creating a new array and copying the cells of the old array to the new one.

An array can be created in two ways. Let's take a look at the way in which we give content to the array at creation. An array of the integer type that consists of 3 cells is defined as follows:

```java
int[] numbers = {100, 1, 42};
```

The type of the Array object is denoted as `int[]`, which stands for an array, the cells of which are of the type int. In the example the name of the array-object is `numbers` and it holds 3 number values `{100, 1, 42}`. The array is formatted with a block, in which the values to be inserted into the array are separated by commas.

The values of the array can be of any variable type that we've seen earlier. Below we've first introduced an array containing character strings and then an array containing floating numbers.

```java
String[] characterStringArray = {"Matti P.", "Matti V."};
double[] floatingNumberArray = {1.20, 3.14, 100.0, 0.6666666667};
```

The cells of the array are referred to with indexes that are integers. The index tells the position of the cell in the array. The first item in an array is in position 0, the next one in position 1, and so forth. When inspecting a certain value of an array, the index is given after the name of the array object in brackets.

```java
// index           0   1    2    3   4   5     6     7
int[] numbers = {100,  1,  42,  23,  1,  1, 3200, 3201};

System.out.println(numbers[0]);    // prints the number in the array's index 0: the number 100
System.out.println(numbers[2]);    // prints the number in the array's index 2, the number 42
```

The size (length) of the array above is 8.

*You'll probably notice that the get-method of ArrayList works pretty much the same as getting from a certain index of an array. Only the notation - the syntax - is different when dealing with arrays.*

Setting an individual value to a certain position in an array happens the same way as with regular variables, only with arrays the index also has to be mentioned. The index is mentioned inside brackets.

```java
int[] numbers = {100,1,42};

numbers[0] = 1;    // setting value 1 to index 0
numbers[1] = 101;  // setting value 101 to index 1

// the numbers array now looks like {1,101,42}
```

If an index points *past an array*, that is, to a cell that doesn't exist, we will get an error: `ArrayIndexOutOfBoundsException`, which means that the index that we pointed at doesn't exist. So we cannot refer to a cell that is past the array - to an index that is smaller than 0, or larger or equals the size of the array.

We'll notice that the array clearly is related to ArrayList. Arrays, as with lists, have their cells in a certain order!

### Iteration of an array

The size of an array object can be found out by typing `array.length` into the code, notice that you don't use parentheses with this one. `array.length()` does not work!

Iterating through the cells of an array is easy to implement with the help of the for-command:

```java
int[] numbers = {1, 8, 10, 3, 5};

for (int i = 0; i < numbers.length; i++) {
    System.out.println(numbers[i]);
}
```

With the help of variable i we go through the indexes 0, 1, 2, 3, and 4, and print the value of the variable in each cell. First `numbers[0]` gets printed, then `numbers[1]` and so forth. The variable `i` stops getting increased when the array has been iterated through, that is when `i`'s value is equal to the length of the array.

When iterating through an array it isn't always necessary to list the indexes of it, the only interesting thing is the values of the array. In this case we can use the for-each-structure - that we became familiar with earlier - to go through the values. Now only the name of a variable is given in the frame of the loop, to which each of the values of the array are set one after the other. The name of the array is separated with a colon.

```java
int[] numbers = {1,8,10,3,5};

for (int number : numbers) {
    System.out.println(number);
}
```

```java
String[] names = {"Juhana L.", "Matti P.", "Matti L.", "Pekka M."};

for (String name : names) {
    System.out.println(name);
}
```

**Notice**: when using a for-each-type of loop you cannot set values to the cells of the array! With the format of the for-sentence we inspect next that can be done too.

### For and array length

Going through all cells of an array with for happens like this:

```java
int[] numbers = {1, 8, 10, 3, 5};

for (int i = 0; i < numbers.length; i++ ) {
    System.out.println(numbers[i]);
}
```

Notice, that in the condition `i < numbers.length` we compare the value of the loop variable to the length we get from the array. The condition should not in any case be "hardcoded" as, for example, `i < 5` because often the length of the array can't be known for sure beforehand.

### Array as a parameter

Arrays can be used - just as any other objects - as a parameters to a method. Notice that, as with all objects, the method gets a reference to an array, so all changes done to the content of the array in the method also show up in the main program.

```java
public static void listCells(int[] integerArray) {

    System.out.println("the cells of the array are: ");
    for( int number : integerArray) {
        System.out.print(number + " ");
    }

    System.out.println("");
}

public static void  main(String[] args) {
    int[] numbers = { 1, 2, 3, 4, 5 };
    listCells(numbers);
}
```

As we already know, the name of the parameter within a method can be freely chosen. The name does not need to be the same as in the one used in calling it. Above, the array is called `integerArray` within the method and the caller of the method knows the array as `numbers`.

{% include_relative exercises/001.md %}
{% include_relative exercises/002.md %}
{: .exercises }

### Creating a new array

If the size of the array isn't always the same, that is, if its size depends on user input for example, the previously introduced way of creating arrays will not do. It is also possible to create a table so that its size is defined with the help of a variable:

```java
int cells = 99;
int[] array = new int[cells];
```

Above we create an array of the type int, that has 99 cells. With this alternative way creation of an array happens just like with any other object; with the command new. Following the new is the type of the array and in the brackets is the size of the array.

```java
int cells = 99;
int[] array = new int[cells]; //creating an array of the size of the value in the 'cells' variable

if(array.length == cells) {
    System.out.println("The length of the array is " + cells);
} else {
    System.out.println("Something unreal happened. The length of the array is something else than " + cells);
}
```

In the following example there is a program that prompts for the user the amount of values and subsequently the values. After this the program prints the values in the same order again. The values given by the user are stored in the array.

```java
System.out.print("How many values? ");
int amountOfValues = Integer.parseInt(reader.nextLine());

int[] values = new int[amountOfValues];

System.out.println("Enter values:");
for(int i = 0; i < amountOfValues; i++) {
    values[i] = Integer.parseInt(reader.nextLine());
}

System.out.println("Values again:");
for(int i = 0; i < amountOfValues; i++) {
    System.out.println(values[i]);
}
```

A run of the program could look something like this:

```output
How many values? ~~4~~
Enter values:
4
8
2
1
Values again:
4
2
8
1
```

### An array as the return value

Since methods can return objects, they can also return arrays. This particular method that returns an array looks like this -- notice that arrays might as well contain objects.

```java
public static String[] giveStringTable() {
    String[] tchrs = new String[3];

    tchrs[0] = "Bonus";
    tchrs[1] = "Ihq";
    tchrs[2] = "Lennon";

    return tchrs;
}

public static void main(String[] args){
    String[] teachers = giveStringTable();

    for ( String teacher : teachers)
        System.out.println( teacher );
}
```

{% include_relative exercises/003.md %}
{: .exercises }
