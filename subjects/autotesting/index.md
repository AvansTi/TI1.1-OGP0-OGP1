---
layout: ogp1
title: Automatic Testing
meta: Put extra info here, like if there any subjects required for this subject
todo: what should be improved in this chapter
---
{% include licence.md %}


## Towards Automatic Tests

Testing a program manually is a hopeless burden. It is possible to automate inputs by setting up a string as a `Scanner` object parameter. The example below shows how it is possible to test automatically the program above.

```java
String input = "translate\n" + "monkey\n"  +
                "translate\n" + "cheese\n" +
                "add\n"  + "cheese\n" + "juusto\n" +
                "translate\n" + "cheese\n" +
                "quit\n";

Scanner reader = new Scanner(input);
Dictionary dictionary = new Dictionary();

TextUserInterface ui = new TextUserInterface(reader, dictionary);
ui.start();
```

The print output contains only the program output, and not the user commands.

```output
Commands:
  add - adds a word couple to the dictionary
  translate - asks for a word and prints its translation
  quit - stops the user interface

Command: Give word: Unknown word!

Command: Give word: Unknown word!

Command: In Finnish: Translation:
Command: Give word: Translation: juusto

Command: Cheers!
```

Giving a string to a `Scanner` class is a way to replace the `String` inputs given through the keyboard. The contents of the `String` variable input "simulates" the user input. `\n` denotes a line break. Each single part of the `input` variable which ends with a line break corresponds to one `nextLine()` input.

It is easy to change the text input, and we can add new words to our dictionary in the following way:

```java
String input = "add\n"  + "cheese\n" + "juusto\n" +
                "add\n"  + "bier\n" + "olut\n" +
                "add\n"  + "book\n" + "kirja\n" +
                "add\n"  + "computer\n" + "tietokone\n" +
                "add\n"  + "auto\n" + "car\n" +
                "quit\n";
```

If you want to test again your program manually, change the `Scanner` object constructor parameter into `System.in`, i.e system input stream.

The program functionality must be checked from the output pane, still. The result can still be confusing at the beginning, because the automatic input does not appear in the output pane at all.

The final goal will be to also automate the testing the program's functionality, so that both testing the program and analising its output text would happen successfully in one click.
