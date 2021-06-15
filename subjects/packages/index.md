---
layout: ogp1
title: Packages
meta: Put extra info here, like if there any subjects required for this subject
todo: what should be improved in this chapter
---
{% include licence.md %}

## Organising Classes into Packages

When we design and implement bigger programs, the number of classes rapidly grows. When the number of classes grows, remembering their functionality and methods becomes more difficult. Giving sensible names to classes helps to remember their funcitonality. In addition to giving sensible names, it is good to split the source code files into packages according to their functionality, use, and other logical reasons. In fact, the *packages* are but folders we use to organise our source code files. Directories are often called folders, both in windows and colloqually. We will use the term directory, anyway.

Programming environments provide made-up tools for package management. So far, we have been creating classes and interfaces only in the *default package* of the *Source Packages* partition. In IntelliJ, we can create a new package by clicking on *Source folder*, and choosing *New -> Package....* In the created package, we can create classes in the same way as we do in the *default package*.

You can read the name of the package that contains a certain class at the beginning of the source code files in the sentence `package packageName` before the other statements. For instance, the below class `Implementation` is contained in the package `library`.

```java
package library;

public class Implementation {

    public static void main(String[] args) {
        System.out.println("Hello packageworld!");
    }
}
```

Packages can contain other packages. For instance, the package definition `package library.domain` means that the package `domain` is contained in the package library. By placing packages into other packages, we design the hierachy of classes and interfaces. For instance, all Java's classes are located in packages that are contained in the package java. The package name domain is often used to represent the storage location of the classes which deal with concepts specific for the domain. For instance, the class `Book` could be stored in the package `library.domain` because it represents a concept specific of the library.

```java
package library.domain;

public class Book {
    private String name;

    public Book(String name) {
        this.name = name;
    }

    public String getName() {
        return this.name;
    }
}
```

We can uses the classes stored in our packages through the `import` statement. For instance, the class `Implementation`, which is contained in the package `library` could make use of a class stored in `library.domain` through the assignment `import library.domain.Book`.

```java
package library;

import library.domain.Book;

public class Implementation {

    public static void main(String[] args) {
        Book book = new Book("The ABC of Packages!");
        System.out.println("Hello packageworld: " + book.getName());
    }
}
```

```output
Hello packageworld: The ABC of Packages!
```

The import statements are defined in our source code file after the package statement but before the class statement. There can be many of them -- for instance, when we want to use different classes. Java's made-up classes are usually stored in `java` package child packages. Hopefully, the statements which appear at the beginning of our classes -- such as `import java.util.ArrayList` and `import java.util.Scanner;` -- are starting to look more meaningful now.

From now on, in *all* our exercises we will use packages. Next, we will create our first packages ourselves.

{% include_relative exercises/001.md %}
{: .exercises }

### A Concrete Directory Construction

All the projects which can be seen are stored in your computer *[file system](http://en.wikipedia.org/wiki/File_system)*. Each project has its own directory (folder) which contains the project directories and files.

The project directory `src` contains the program source code. If a class package is a library, it is located in the directory library of the project source code directory `src`. If you are interested in it, it is possible to have a look at the concrete project structure in IntelliJ, by going to the *Files* tab which is next to the *Projects* tab. If you can't see the *Files* tab, you can display it by choosing *Files* from the *Window* menu.

Application development is usually done through the *Projects* tab, where NetBeans has hidden the project files which the programmer doesn't have to care about.

### Visibility Definitions and Packages

We have already managed to know two visibility definitions. The method and variables with the visibility definition `private` are visible only inside the class that defines them. They cannot be used outside the class. Differently, the method and variables with visibility definition `public` are visible for any class.

```java
package library.ui;

public class UserInterface {
    private Scanner reader;

    public UserInterface(Scanner reader) {
        this.reader = reader;
    }

    public void start() {
        printTitle();

        // more functionality
    }

    private void printTitle() {
        System.out.println("***********");
        System.out.println("* LIBRARY *");
        System.out.println("***********");
    }
}
```

The object constructor and method `start` of the above class `UserInterface` can be called from whatever program. The method `printTitle` and the variable `reader` can be used only inside their class.

When we want to assign package visibility to a variable or a method, we do not need to use any prefix. We can modify the example above assigning package visibility to the method `printTitle`.

```java
package library.ui;

public class UserInterface {
    private Scanner reader;

    public UserInterface(Scanner reader) {
        this.reader = reader;
    }

    public void start() {
        printTitle();

        // more functionality
    }

    void printTitle() {
        System.out.println("***********");
        System.out.println("* Library *");
        System.out.println("***********");
    }
}
```

Now, the classes *inside the same package* can use the method `printTitle`.

```java
package library.ui;

import java.util.Scanner;

public class Main {

    public static void main(String[] args) {
        Scanner reader = new Scanner(System.in);
        UserInterface userInterface = new UserInterface(reader);

        userInterface.printTitle(); // it works!
    }
}
```

If the class is in a different package, the method `printTitle` can't be used.

```java
package library;

import java.util.Scanner;
import library.ui.UserInterface;

public class Main {

    public static void main(String[] args) {
        Scanner reader = new Scanner(System.in);
        UserInterface userInterface = new UserInterface(reader);

        userInterface.printTitle(); // it doesn't work  !
    }
}
```
