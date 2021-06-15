---
layout: default
title: Break and Continue
meta: 
todo: 
---
{% include licence.md %}

## Changing the flow of execution in a loop

#### Break

It is also possible to change the flow of execution in a loop. This is done with the `break` and `continue` keywords.

The `break` keyword immediately breaks the loop, and jumps out of the loop. This is usually used as little as possible, as the code execution can become very chaotic with a lot of `break` commands. An example of using this is rewriting the code from section 11.3, which can also be written as

```java
System.out.println("Type your age ");
int age;
while (true) {
    age = Integer.parseInt(reader.nextLine());

    if (age >= 5 && age <= 85) {  // age between 5 AND 85
        break;  // end the loop
    }

    System.out.println("You are lying!");
    if (age < 5) {
        System.out.println("You are so young that you cannot know how to write!");
    } else {  // that means age is over 85
        System.out.println("You are so old that you cannot know how to use a computer!");
    }

    System.out.println("Type your age again: ");
}

System.out.println("Your age is " + age);
```


Note that this example uses a `while(true)` command, which is another bad practice

#### Continue

The `continue` statement jumps back to the beginning of the loop. This can be used to 'skip' certain values of variables. An example

```java
int i = 0;
while (i < 100) {
    i++;
    if(i % 2 == 0) {
        continue;
    }
    if(i % 3 == 0) {
        continue;
    }
    if(i % 5 == 0) {
        continue;
    }
    System.out.println(i);
}
```
{: .interactive .hideStack #break-continue-5 }

This example will output all values that are not dividable by 2, 3, 5. Note that the output does not include 0, as this is skipped by the `i++` command. 

{% include_relative exercises/001.md %}
{: .exercises }

### Note: creating a program in small steps
>In these exercises we actually created one single program, but programming happened in very small steps. This is *ALWAYS* the preferred way to program.
>
>When you are programming something, no matter if it is an exercise or a project of your own, it is advised to do it in very tiny pieces. Do not ever try to solve the whole problem in one go. Start with something easy, something you know that you can do. In this recent set of exercises, for example, we focused first on stopping the program when the user types -1. When one part of the program is complete and working, we can move on to work out the solution for the next sub-problem of the big main problem.
>
>Some of the exercises in this course are sliced into smaller pieces like the set of exercises we just introduced. Usually the pieces need to be sliced again into smaller pieces depending on the problem. It is advised that you execute the whole program after almost every new line of code you write. This enables you to be sure that your solution is going in the right and working direction.
