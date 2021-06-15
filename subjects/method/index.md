---
layout: default
title: Methods
meta: 
todo: 
---
{% include licence.md %}

## Methods

We have so far used many different commands of Java: assignment, calculations, comparison, if structures and while structures. We have been using a "command" `System.out.println()` to print text. We can also count the maximum of two numbers with the help of the "command" `Math.max()`. We are also familiar with `reader.nextLine()`, usually seen together with `Integer.parseInt()`.

If we take a closer look, we notice that those commands differ from if and while (etc). The first difference is that after the command there are brackets () and sometimes an input for the command inside those brackets. Actually, the commands ending with brackets are not called commands, but **methods**.

Technically speaking, a method is a piece of code that can be called from different places of the program code. The line of code `System.out.println("I am a parameter given to the method!")` means that we call a method that actually handles the printing. After the method has been executed we go back to where we called the method, and continue executing. The input given to the method inside the brackets is called a *method parameter*.

In addition to a parameter, the method can also have a return value, for example, a familiar line of code:

```java
int number = Integer.parseInt( reader.nextLine() );
```

includes two method calls. First the inner method `reader.nextLine` is called. That method has the integer typed by the user as a return value. Next the outer method `Integer.parseInt` is called. As a parameter for that method there is the string of characters that was received from the `reader.nextLine` method as a return value. The return value for the method `Integer.parseInt` is the string of characters transformed into an integer (whole number).

Method names also seem to include a dot, for example `reader.nextLine()`. Actually the method name starts after the dot, here it is `nextLine()`. The first part of the command that comes before the dot shows whose method is in question. Here the method belongs to the reader, which means that we have the *reader*'s method `nextLine`. Later we will learn more precisely about the owner of the method (or the name on the left side of the dot). An attentive reader will notice that the method `System.out.println()` has two dots. Here, the method name is `println` and `System.out` is the owner of the method. Roughly `System.out` means the computer monitor.

This far we have been using ready-made methods from Java libraries. Next we will learn how to create our own methods.

## Self-written methods

This far we have been using a programming style where code is written (and read and executed) from top to bottom.

It was mentioned before that "a method is a piece of code that can be called from different places of the program code". Ready-made methods of Java have been used since our very first program.

In addition to using these ready-made methods programmers can write their own methods for programs to call. In the real world, it is really exceptional if the program does not include any self-written methods. From now on almost every program we create during this course will include self-written methods.

The methods are written in the program body outside the main's braces ( { and } ) but still inside the outermost braces, for example like this: :

```java
import java.util.Scanner;

public class ProgramBody {
    public static void main(String[] args) {
        Scanner reader = new Scanner(System.in);
        // program code
    }

    // self-written methods
}
```

Let us create a method `greet`.

```java
public static void greet() {
    System.out.println("Greetings from the world of methods!");
}
```

And let us place it in the right spot.

```java
import java.util.Scanner;

public class ProgramBody {
    public static void main(String[] args) {
        Scanner reader = new Scanner(System.in);
        // program code
    }

    // self-written methods
    public static void greet() {
        System.out.println("Greetings from the world of methods!");
    }
}
```

In order to define a new method we need to write two things. In the first row of the method definition, you will find the name of the method, in this case greet. On the left side of the name you will find the definitions `public static void`. On the next line, the code block marked by the braces ({ and }). Inside it, the method's code, or the commands that will be executed when the method is called. Our method `greet` only writes one line of text to the screen.

It is easy to call a self-written method. It happens by writing the method name, brackets () and a semicolon. In the next example main (or the main program) calls for our method, first once and then several times.

```java
import java.util.Scanner;

public class ProgramBody {
    public static void main(String[] args) {
        Scanner reader = new Scanner(System.in);

        // program code
        System.out.println("Let us try if we can get to the method world:");
        greet();

        System.out.println("It seems like we can, let us try again:");
        greet();
        greet();
        greet();
    }

    // self-written methods
    public static void greet() {
        System.out.println("Greetings from the world of methods!");
    }
}
```
{: .interactive #method-1 }

What is noteworthy here is the execution order of the program code. The execution starts with the main program's (or main's) lines of code, from top to bottom, one by one. When the line of code to be executed happens to be a method call, the lines of code in the method block are executed again one by one. When the method block ends, the execution continues from the place where the method was called. To be exact, the execution continues from the next line after the original method call.

To be even more exact, the main program is also a method. When the program starts, the operation system calls for the main method. That means that the main method is the starting point of the program and the execution starts from the first code line of main. The program execution ends when it reaches the end of main.

From now on when we introduce methods, we will not point out that they need to be written in the right place inside the program code. For example, a method cannot be defined inside another method.


{% include_relative exercises/001.md %}
{% include_relative exercises/002.md %}
{: .exercises }

### Method parameters

We can make our methods more useful by giving it *parameters*! Parameters are variables that we define inside brackets in the first line, just after the method name. When the method is called, the parameters are assigned values.

In the next example we define a method with a parameter, its name will be greet and its parameter will be a variable of the type String called `name`.

```java
public static void greet(String name) {
    System.out.println("Hi " + name + ", greetings from the world of methods!");
}
```

Let us next call the `greet` method so that on the first try we give its parameter the value `Matt` and on the second try `Arthur`.

```java
public static void main(String[] args) {
    greet("Matt");
    greet("Arthur");
}
```

```output
Hi Matt, greetings from the world of methods!
Hi Arthur, greetings from the world of methods!
```

More complicated expressions can also be used as a parameter for our self-written methods, the same way we used them together with the ready-made `System.out.println()` method.

```java
public static void main(String[] args) {
    String name1 = "Anne";
    String name2 = "Green";
    greet( name1 + " " + name2 );

    int age = 24;
    greet("John " + age + " years");
}
```

```output
Hi Anne Green, greetings from the world of methods!
Hi John 24 years, greetings from the world of methods!
```

In both cases the method has only one parameter. The value for the parameter is calculated before calling the method. In the first case the parameter value comes from the String concatenation (a cool word that means putting the text together) `name1 + " " + name2`. The value for the concatenation is *Anne Green*. In the second case we get the parameter value from the String concatenation `"John " + age + " years"`.

### Many parameters

A method can be defined to have more than one parameter. In this case, the parameters are always listed in the same order.

```java
public static void greet(String name, String greetingsFrom) {
    System.out.println("Hi " + name + ", greetings from " + greetingsFrom);
}

public static void main(String[] args)
{
    String who = "Matt";
    String greetings = "Alabama";

    greet(who, greetings);
    greet(who, greetings + " from Nevada");
}
```
{: .interactive #method-2 }

In the last `greet` function (or method) call the second parameter is formed by concatenating (or adding) the text “from Nevada” to the variable `greetings`. This is done before the actual function call.

```output
Hi Matt, greetings from Alabama
Hi Matt, greetings from Alabama from Nevada
```

### Method calling another method

Methods can also be called outside of main. Methods can call each other! Let us create a method greetManyTimes that greets the user many times getting assistance from the method `greet`:

```java
public static void greet(String name) {
    System.out.println("Hi " + name + ", greetings from the world of methods!");
}

public static void greetManyTimes(String name, int times) {
    int i = 0;
    while ( i < times ) {
        greet(name);
        i++;
    }

}

public static void main(String[] args) {
    greetManyTimes("Anthony", 3);
    System.out.println("and");
    greetManyTimes("Martin", 2);
}
```
{: .interactive .hideStack #method-3 }

{% include_relative exercises/003.md %}
{% include_relative exercises/004.md %}
{% include_relative exercises/005.md %}
{% include_relative exercises/006.md %}
{: .exercises }


## Math Library

A lot of functionality can be implemented by now, using the basic code stuctures that we've encountered so far. We could for example, write a method to determine the [absolute value](https://en.wikipedia.org/wiki/Absolute_value) of a number. The code for such a method could be as follows

```java
public static int abs(int number)
{
    if(number < 0) {
        return -number;
    } else {
        return number;
    }
}
```

Writing these methods for all basic math concepts is not very hard, but it is a lot of work to write them. Fortunately, a lot of this has already been written, and combined in the `Math` structure. We can find a lot of information on this in the [documentation](https://docs.oracle.com/javase/8/docs/api/java/lang/Math.html). In this documentation, we can typically find some very important information on these method. The document starts with a long list of available methods, followed by a short description. Clicking on a method will show a longer description

![abs](images/2_8_abs.png)

In the line `public static int abs(int a)` we can see the parameter type, and a description of the parameter. We can also see the *return type*, which will be covered next week. Also a precise description is available, to see exactly what this method will do.

Some convenient methods are:

- `abs` Returns the absolute value of a value.
- `ceil` Returns the smallest (closest to negative infinity) double value that is greater than or equal to the argument and is equal to a mathematical integer.
- `cos` Returns the trigonometric cosine of an angle. (parameter is in radians)
- `floor` Returns the largest (closest to positive infinity) double value that is less than or equal to the argument and is equal to a mathematical integer.
- `log` Returns the natural logarithm (base e) of a double value.
- `max` Returns the greater of two values.
- `min` Returns the smaller of two values.
- `pow` Returns the value of the first argument raised to the power of the second argument.
- `random` Returns a double value with a positive sign, greater than or equal to 0.0 and less than 1.0.
- `round` Returns the closest int to the argument, with ties rounding to positive infinity.
- `signum` Returns the signum function of the argument; zero if the argument is zero, 1.0 if the argument is greater than zero, -1.0 if the argument is less than zero.
- `sin` Returns the trigonometric sine of an angle. (parameter is in radians)
- `sqrt` Returns the correctly rounded positive square root of a double value.
- `tan` Returns the trigonometric tangent of an angle.
- `toDegrees` Converts an angle measured in radians to an approximately equivalent angle measured in degrees.
- `toRadians` Converts an angle measured in degrees to an approximately equivalent angle measured in radians.

Also you can use `Math.PI` as a value of $$\pi$$

