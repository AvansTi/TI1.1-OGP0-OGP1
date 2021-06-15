---
layout: default
title: Methods and copying parameters
meta: 
todo: 
---
{% include licence.md %}

## Methods and copying parameters

Let us focus on a couple of details concerning methods.

In section 15 was an example, in which we tried to change the value of a main program variable inside a method.

```java
public static void main(String[] args) {
    int number = 1;
    addThree();
    System.out.println("Main program variable number holds the value: " + number);
}

public static void addThree() {
    number = number + 3;
}
```
  
This program of ours does not work. The reason is that the method cannot access the main program variable `number`.

This is because main program variables are not visible to methods. More generally: no method variable is visible to other methods. As the main program `main` is also a method, this constraint holds for the main program as well. The only way to give information to a method is through parameters.

Let us try to fix the above example by passing the main program variable `number` to the method as a parameter.

```java
public static void main(String[] args) {
    int number = 1;
    addThree(number);
    System.out.println(number);  // prints 1, the value did not change
}

public static addThree(int number) {
    number = number + 3;
}
```
  
Still, the program does not function the way we want. The method parameters are different variables than the ones introduced in the main program. In the previous example, the method increments a variable with the same name as the main program variable. The parameter has the same name, but is not the same as the main program variable `number`.

When a parameter is given to a method, the value of the parameter *is copied into* a new variable and that new variable is the one the method uses. In the example above, the variable `number` that was given to the method `addThree` as a parameter, will be copied and then the copy is actually handed out for the method to use. The method uses a copy of the variable from the main program, not the original variable. The main program variable `number` stays unchanged.

We can imagine that the main program method `main` and the method `addThree` both work in their own parts of the computer memory. In the picture below, there is a "box" for the value of the variable number of the main method. When the method is called, a new "box" named `number` will be created and the main value of the method variable `number` will be copied into it. In this example, the number is 1. Both variables that are called `number` are separate, therefore when the method `addThree` changes the value of its own variable called `number` it does not affect the variable `number` in the main program.

The picture below will demonstrate what happens.

![memory](images/19_copy.png)

The method can still naturally pass information to the caller, which happens by using a return value (i.e. using a `return` command to return a variable with a value). We can get the previous example to work by changing the code a little bit:

```java
public static void main(String[] args) {
    int number = 1;
    number = addThreeAndReturn(number);

    System.out.println(number);  // prints 4, because number has the method return value as its value
}

public static int addThreeAndReturn(int number) {
    number = number + 3;

    return number;
}
```
  
The method still uses the copy of the main program variable `number`. In the main program, we assign the variable `number` the method return value as a new value, so that we can get the change to take effect in the main program. Note that the name of the method variable plays no role here. The code works exactly the same regardless of the variable names. Here follows an example:

```java
public static void main(String[] args) {
    int number = 1;
    number = addThreeAndReturn(number);

    System.out.println(number);
}

public static int addThreeAndReturn(int incremented) {
    incremented = incremented + 3;

    return incremented;
}
```

We have now found out that the parameters in methods are different variables than the variables introduced in the method call. Only the parameter value gets copied from the caller to the method.

Unfortunately this is not the whole story. If a method gets an `ArrayList` as a parameter, the method sees the original list and all the changes the method makes will take effect everywhere.

```java
public static void removeFirst(ArrayList<Integer> list) {
    list.remove(0); // removes the number from index 0
}
  
public static void main(String[] args) {
    ArrayList<Integer> numbers = new ArrayList<Integer>();
    numbers.add(4);
    numbers.add(3);
    numbers.add(7);
    numbers.add(3);

    System.out.println(numbers); // prints [4,3,7,3]

    removeFirst(numbers);

    System.out.println(numbers); // prints [3,7,3]
}
```

Unlike a parameter of `int` type, a list will not be copied and therefore the method makes changes to the original list given as a parameter.

The picture below will clarify the example. `ArrayList` does not live in an imagined "box" like an `int`. The variable name in the example `numbers` is only a *reference* that refers to the place where the ArrayList is. One way to visualize this is that an `ArrayList` is connected with a wire. The name of the `ArrayList` is a "wire", and the list itself is located "at the other end of the wire". When we give the ArrayList to a method as a parameter, we actually give the method a wire. When the method uses its parameter, it finds the original list at the other end of this wire. Actually the main program and the method do have separate wires, but both wires have the same original list at the end of them and all the changes will be made directly to the original list. During and after this week we will find out that many things in Java are "connected with a wire".

![reference](images/19_reference.png)

Note that again the parameter name inside the method can be anything. It does not need to be the same as the name in the main program (or other method that calls it). In the example above, the method uses the name list but the method caller sees the same list with a different name: `numbers`.

Now, you probably start to wonder why does the value of the parameter get copied and the original variable stay intact when the parameter is of int type, but the original list is given to the method when the parameter is of `ArrayList` type? In Java only the values of *primitive data types* (which are `int`, `double`, `char`, `boolean` and a couple of others that we have not yet discussed) get copied to the method. When the method parameters are of other types only the references are copied to the method. A reference is like a "wire", therefore the method can access the list using it directly. The variables that are not of primitive data types are of **reference data types** and are "wired" just like the ArrayList in the previous example. The method is given the wire and the method can access the parameter directly.

{% include_relative exercises/001.md %}
{% include_relative exercises/002.md %}
{: .exercises }