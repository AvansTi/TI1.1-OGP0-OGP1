---
layout: ogp1
title: Single Responsibility Principle
meta: Put extra info here, like if there any subjects required for this subject
todo: what should be improved in this chapter
---
{% include licence.md %}

## Single Responsibility Principle

When we design bigger programs, we often reason about what class has to deal with what task. If we delegate the implementation of the whole program to one class, the result is inevitably chaos. A sector of software design, *object-oriented design*, includes the *Single Responsibility Principle*, which we should follow.

The Single Responsibility Principle states that each class should have only one clear role. If the class has one clear role, *modifying* that role is easy, and only one class will have to be modified. *Each class should have only one reason to be modified..*

Let us focus on the following class `Worker`, which has methods to calculate his salary and to report his working hours.

```java
public class Worker {
    // object variables

    // worker's constructor and methods

    public double calculateSalary() {
        // the logic concerning salary count
    }

    public String reportHours() {
        // the logic concerning working hours bookkeeping
    }
}
```

Even if the examples above do not show the concrete implementations, an alarm should go off. Our `Worker` class has at least three different responsibilities. It represents a worker, it performes the role of a salary calculator, and the role of a working hour bookkeeping system by reporting working hours. The class above should be split into three: one should represent the worker, another should represent the salary calculator, and the third should deal with time bookkeeping.

```java
public class Worker {
    // object variables

    // worker's constructor and methods
}
```

```java
public class SalaryCalculator {
    // object variables

    // methods for salary count

    public double calculateSalary(Person person) {
        // salary calculation logic
    }
}
```

```java
public class TimeBookkeeping {
    // object variables

    // methods concerning time bookkeeping

    public String createHourReport(Person person) {
        // working hours bookeeping logic
    }
}
```

*Each variable, each code raw, each method, each class, and each program should have only one responsibility. Often a "better" program stucture is clear to the programmer only once the program is implemented. This is completely acceptable: even more important it is that we always try to change a program to make it clearer. **Always refactor -- i.e. always improve your program when it is needed!***
