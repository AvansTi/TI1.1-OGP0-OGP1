---
layout: default
title: while loops
meta: 
todo: 
---
{% include licence.md %}

## Introduction to loops

Conditional statements allow us to execute different commands based on the conditions. For example, we can let the user login only if the username and password are correct.

In addition to conditions we also need repetitions. We may, for example, need to keep asking the user to input a username and password until a valid pair is entered.

The most simple repetition is an infinite loop. The following code will print out the string *I can program!* forever or "an infinite number of times":

```java
while (true) {
    System.out.println("I can program!");
}
```

In the example above, the `while (true)` command causes the associated block (i.e. the code between the curly braces `{}`) to be *looped* (or repeated) infinitely.

We generally do **not** want an infinite loop. The loop can be interrupted by changing the condition in the while-loop

```java
boolean running = true;
while (running) {
    System.out.println("I can program!");

    System.out.print("Continue? ('no' to quit)? ");
    String command = reader.nextLine();
    if (command.equals("no")) {
        running = false;
    }
}

System.out.println("Thank you and see you later!");
```

Now the loop progresses like this: First, the program prints *I can program!*. Then, the program will ask the user if it should continue. If the user types *no*, the variable `running` is set to false, and the loop stops and *Thank you and see you again!* is printed. Take note that the commands in the loop will continue to execute, and the loop will stop at the end of the code block in the loop. As there is no other code in the loop, it stops immediately 

```output
I can program!
Continue? ('no' to quit)? ~~yeah~~
I can program!
Continue? ('no' to quit)? ~~jawohl~~
I can program!
Continue? ('no' to quit)? ~~no~~
Thank you and see you again!
```

Many different things can be done inside a loop. Next we create a simple calculator, which performs calculations based on commands that the user enters. If the command is *quit*, the variable running will be set to false, and the program will quit. Otherwise two numbers are asked. Then, if the initial command was *sum*, the program calculates and prints the sum of the two numbers. If the command was *difference*, the program calculates and prints the difference of the two numbers. If the command was something else, the program reports that the command was unknown.

```java
System.out.println("welcome to the calculator");
boolean running = true;
while (running) {
    System.out.print("Enter a command (sum, difference, quit): ");
    String command = reader.nextLine();
    if (command.equals("quit")) {
        running = false;
    } else {
        System.out.print("enter the numbers");
        int first = Integer.parseInt(reader.nextLine());
        int second = Integer.parseInt(reader.nextLine());

        if (command.equals("sum") ) {
            int sum = first + second;
            System.out.println( "The sum of the numbers is " + sum );
        } else if (command.equals("difference")) {
            int difference = first - second;
            System.out.println("The difference of the numbers is " + difference);
        } else {
            System.out.println("Unknown command");
        }
    }
}

System.out.println("Thanks, bye!");
```

> Note that this code uses the `reader` to read user input. To make this reader object, don't forget to add the following line to your code:
>
> ```java
> Scanner reader = new Scanner(System.in);
>```
>
{: .tip}

{% include_relative exercises/001.md %}
{% include_relative exercises/002.md %}
{% include_relative exercises/003.md %}
{% include_relative exercises/004.md %}
{: .exercises }

## while conditions

The `running` variable is not the only way to end a loop. A common structure for a loop is `while (condition)`, where the condition can be **any statement with a truth value**. This means that the condition works exactly like conditions in an `if` statements.

In the following example, we print the numbers 1, 2, …, 10. When the value of the variable number increases above 10, the condition of the while statement is no longer true and the loop ends.

```java
int number = 1;

while (number < 11) {
    System.out.println(number);
    number++;  // number++ means the same as number = number + 1
}
```
{: .interactive .hideStack #while-1 }

The example above can be read "as long as the variable number is less than 11, print the variable and increment it by one".

Above, the variable `number` was incremented in each iteration of the loop. Generally the change can be anything, meaning that the variable used in the condition does not always need to be incremented. For example:

```java
int number = 1024;

while (number >= 1) {
    System.out.println(number);
    number = number / 2;
}
```
{: .interactive .hideStack #while-2 }


>Complete the following exercises using the while statement:
{% include_relative exercises/005.md %}
{% include_relative exercises/006.md %}
{% include_relative exercises/007.md %}
{% include_relative exercises/008.md %}
{% include_relative exercises/009.md %}
{: .exercises }


### Infinite loops

One of the classic errors in programming is to accidentally create an infinite loop. In the next example we try to print "Never again shall I program an eternal loop!" 10 times:

```java
int i = 0;

while (i < 10) {
    System.out.println("Never again shall I program an eternal loop!");
}
```

The variable `i`, which determines is supposed to index the loops, is initially set to 0. The block is looped as long as the condition `i < 10` is true. But something funny happens. Because the value of the variable `i` is never changed, the condition stays true forever.

### Ending a while loop

So far, we have used the while loop with a structure similar to this:

```java
int i = 1;
while (i < 10) {
    // Some code.
    i++;
}
```
{: .interactive .hideStack #while-3 }

With the structure above, the variable `i` remembers the number of times the the loop has been executed. The condition to end the loop is based on comparing the value of `i`.

Let us now recall how a while loop is stopped. Ending a while loop does not always need to be based on the amount of loops. The next example program asks for the user's age. If the given age is not in the range 5-85, the program prints a message and asks for the user's age again. As you can see, the condition for the while loop can be any expression that results in a boolean (truth value).

```java
System.out.println("Type your age: ");

int age = Integer.parseInt(reader.nextLine());

while (age < 5 || age > 85) {  // age less than 5 OR greater than 85
    System.out.println("You are lying!");
    if (age < 5) {
        System.out.println("You are so young that you cannot know how to write!");
    } else if (age > 85) {
        System.out.println("You are so old that you cannot know how to use a computer!");
    }

    System.out.println("Type your age again: ");
    age = Integer.parseInt(reader.nextLine();
}

System.out.println("Your age is " + age);
```
