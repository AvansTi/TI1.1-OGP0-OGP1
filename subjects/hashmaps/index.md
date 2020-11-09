---
layout: ogp1
title: Hashmaps
meta: Put extra info here, like if there any subjects required for this subject
todo: what should be improved in this chapter
---
{% include licence.md %}
---
## HashMaps

[HashMap](https://docs.oracle.com/javase/8/docs/api/java/util/HashMap.html) is one of Java's most useful data structures. The idea behind `HashMap` is we define an index for an object key - a unique value, for instance a social security number, a student number, or a phone number. We call *hashing* the process of changing a key into an index, or simply to define an index. The hashing happens thanks to a particular function which makes sure that we get always the same index with a known key.

Adding and retrieving items based on the keys allows for a particularly quick search process. Instead of parsing the table items one by one (in the worst case we would have to go through all the items), and instead of looking for a value with a binary search (in which case we would have to go through a number of items which would depend on the logarithm of the table size), we can look at only one table index and check whether a value is mapped to that index.

HashMap uses the `Object` class `hashCode()` method to find a key value. Every `HashMap` subclass will inherit the `hashCode()` method. However, we will not go deep into `HashMap` workings in this course.

Java's `HashMap` class encapsulates - or hides - the way it works, and it returns made-up methods ready to use.

When we create a `HashMap` we need two **type parameters**, a type for the key variable, and a type for the stored object. The following example uses a String-type object as key, and a String-type object as the stored object.

```java
HashMap<String, String> numbers = new HashMap<String, String>();
numbers.put("One", "Yksi");
numbers.put("Two", "Kaksi");

String translation = numbers.get("One");
System.out.println(translation);

System.out.println(numbers.get("Two"));
System.out.println(numbers.get("Three"));
System.out.println(numbers.get("Yksi"));
```

```output
Yksi
Kaksi
null
null
```

In the example, we create a `HashMap` where both the key and the stored object are strings. We add information to the `HashMap` with the `put()` method, which receives the references to the key and to the stored object as parameter. The method `get()` returns either the reference to the key given as parameter or a `null` value in case the key was not found.

Each key is mapped to one value, within the `HashMap`. If we store a new value with an already existing key, the old value is lost.

```java
HashMap<String, String> numbers = new HashMap<String, String>();
numbers.put("One", "Yksi");
numbers.put("Two", "Kaksi");
numbers.put("One", "Uno");

String translation = numbers.get("One");
System.out.println(translation);

System.out.println(numbers.get("Two"));
System.out.println(numbers.get("Three"));
System.out.println(numbers.get("Yksi"));
```

Because the key "One" is assigned a new value, the print output of the example is like the following.

```output
Uno
Kaksi
null
null
```

{% include_relative exercises/001.md %}
{: .exercises }

### Book Search through HashMap

Let us go deeper into `HashMap` workings with the help of the following example. Books can be retrieved based on their name, which acts as book key. If we find a book for the given name, we obtain the respective reference, as well as the book details. Let us create the example class `Book`, which has a name and the book contents as object variables.

```java
public class Book {
    private String name;
    private String contents;
    private int publishingYear;

    public Book(String name, int publishingYear, String contents) {
        this.name = name;
        this.publishingYear = publishingYear;
        this.contents = contents;
    }

    public String getName() {
        return this.name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getPublishingYear() {
        return this.publishingYear;
    }

    public void setPublishingYear(int publishingYear) {
        this.publishingYear = publishingYear;
    }

    public String getContents() {
        return this.contents;
    }

    public void setContents(String contents) {
        this.contents = contents;
    }

    public String toString() {
        return "Name: " + this.name + " (" + this.publishingYear + ")\n"
                + "Contents: " + this.contents;
    }
}
```

In the following example, we create a `HashMap` which makes use of the book name - a String-type object - and stores the references which point to `Book`-objects.

```java
HashMap<String, Book> bookCollection = new HashMap<String, Book>();
```

The `HashMap` above has a `String` object as key. Let us extend our example so that we would add two books to our book collection, "Sense and Sensibility" and "Pride and Prejudice".

```java
Book senseAndSensibility = new Book("Sense and Sensibility", 1811, "...");
Book prideAndPrejudice = new Book("Pride and Prejudice", 1813, "....");

HashMap<String, Book> bookCollection = new HashMap<String, Book>();
bookCollection.put(senseAndSensibility.getName(), senseAndSensibility);
librabookCollectionry.put(prideAndPrejudice.getName(), prideAndPrejudice);
```

Books can be retrieved from the book collection based on their name. A search for the book "Persuasion" does not return a corresponding entry, in which case the `HashMap` returns a `null` reference. However, the book "Pride and Prejudice" was found.

```java
Book book = bookCollection.get("Persuasion");
System.out.println(book);
System.out.println();
book = bookCollection.get("Pride and Prejudice");
System.out.println(book);
```

```output
null

Name: Pride and Prejudice (1813)
Contents: ...
```

HashMaps are useful when we know the key to use for our search. Keys are always unique, and it is not possible to store more than one object together with one key alone. The object which we store can still be a *list* or another `HashMap`, of course!

### Library

The problem with the book collection above is that we must remember the correct book name when we search for it, character by character. Java built-in `String` class provides us the tools for this. The `toLowerCase()` method turns a string's characters to lower case, and the `trim()` method deletes the white spaces at the beginning and at the end of the string. Computer users tend to write white spaces at the beginning or end of a text, involuntarily.

```java
String text = "Pride and Prejudice ";
text = text.toLowerCase(); // the text is now "pride and prejudice "
text = text.trim() // the text is now "pride and prejudice"
```

Let us create the the class `Library`, which encapsulates a `HashMap` containing books, and allows for book search regardless of its spelling. Let us add the methods `addBook(Book book)` and `removeBook(String bookName)` to our Library class. It's already clear that we would need various different methods to clean a string. Therefore, we can create a separate method called `private String stringCleaner(String string)`.

```java
public class Library {
    private HashMap<String, Book> collection;

    public Library() {
        this.collection = new HashMap<String, Book>();
    }

    public void addBook(Book book) {
        String name = stringCleaner(book.getName());

        if(this.collection.containsKey(name)) {
            System.out.println("The book is already in the library!");
        } else {
            collection.put(name, book);
        }
    }

    public void removeBook(String bookName) {
        bookName = stringCleaner(bookName);

        if(this.collection.containsKey(bookName)) {
            this.collection.remove(bookName);
        } else {
            System.out.println("The book was not found, you can't remove it!");
        }
    }

    private String stringCleaner(String string) {
        if (string == null) {
            return "";
        }

        string = string.toLowerCase();
        return string.trim();
    }
}
```

We implement our search functionality so that we can retrieve a book using a hash algorithm based on the book name.

```java
public Book getBook(String bookName) {
    bookName = stringCleaner(bookName);
    return this.collection.get(bookName);
}
```

The method above returns the wanted book when this is found, otherwise it returns a `null` value. We can also also go through all the collection keys one by one, and look for the beginning characters of the book's name. In this way, we would actually fail to capitalise on HashMap performance speed because, in the worst case, we would need to go through all the book names. Search based on the beginning characters of a string is possible through the `keySet()` method. The `keySet()` method returns a set of keys, which can be parsed with the for each loop.

```java
public Book getBookUsingItsBeginningCharacters(String beginning) {
    beginning = stringCleaner(beginning);

    for (String key: this.collection.keySet()) {
        if (key.startsWith(beginning)) {
            return this.collection.get(key);
        }
    }

    return null;
}
```

Let's leave the method above out of our library for now. Our library is still lacking an essential feature concerning book addition. Let us create the method `public ArrayList<Book> bookList()`, which returns a list of the books in our library. The method `bookList()` makes use of the `values()` method, which is provided by `HashList`. The `values()` method returns a set of our library books, which can be given as parameter to the constructor of an `ArrayList` class.

```java
public class Library {
    private HashMap<String, Book> collection;

    public Library() {
        this.collection = new HashMap<String, Book>();
    }

    public Book getBook(String bookName) {
        bookName = stringCleaner(bookName);
        return this.collection.get(bookName);
    }

    public void addBook(Book kirja) {
        String name = stringCleaner(book.getName());

        if(this.collection.containsKey(name)) {
            System.out.println("The book is already in the library!");
        } else {
            this.collection.put(name, book);
        }
    }

    public void removeBook(String bookName) {
        bookName = stringCleaner(bookName);

        if(this.collection.containsKey(bookName)) {
            this.collection.remove(bookName);
        } else {
            System.out.println("The book was not found, you can't remove it!");
        }
    }

    public ArrayList<Book> bookList() {
        return new ArrayList<Book>(this.collection.values());
    }

    private String stringCleaner(String string) {
        if (string == null) {
            return "";
        }

        string = string.toLowerCase();
        return string.trim();
    }
}
```

Among the programming principles, there is the so called *DRY* principle (Don't Repeat Yourself), according to which we try to avoid having code repeat in different places. Turning a string to lower case, and its *trimming* - removing white spaces from the beginning and the end of a string - would have ocurred several different places without the `stringCleaner()` method. We might hardly notice we are repeating the same code as we are writing. It is only afterwards we may see the repeated code has snuck in there. That the repetition happens is not in itself bad, however. The most important thing is that we clean our code as soon as we notice the need.

### Original-Type Variables in a HashMap

Both `HashMap` keys and stored objects are reference-type variables. If we want to use an original-type variable as key or stored value, we can use their reference-type equivalent. Some are introduced below.

| Original-type | Reference-type equivalent                                                       |
|---------------|---------------------------------------------------------------------------------|
| int           | [Integer](https://docs.oracle.com/javase/7/docs/api/java/lang/Integer.html)     |
| double        | [Double](https://docs.oracle.com/javase/7/docs/api/java/lang/Double.html)       |
| char          | [Character](https://docs.oracle.com/javase/7/docs/api/java/lang/Character.html) |

In fact, Java automatically encapsulates original-type values and translates them into reference-type values when needed. Even though the number 1 is an original-type variable, it can be used as an `Integer` key directly in the following way.

```java
HashMap<Integer, String> table = new HashMap<Integer, String>();
table.put(1, "Be!");
```

In Java, the automatic translation of original-type variables into reference-type ones is called *auto-boxing*, i.e. allocation into a slot. The same process also works in the opposite way. We can create a method which returns a `HashMap` containing an `Integer`. In the following example, the automatic translation happens inside the method `addTwitch`.

```java
public class TwitchRegister {
    private HashMap<String, Integer> twitched;

    public NumberBookkeeping() {
        this.twitched = new HashMap<String, Integer>();
    }

    public void addTwitch(String name, int number) {
        this.twitched.put(name, number);
    }

    public int lastTwitch(String name) {
        this.twitched.get(name);
    }
}
```

Even though the `HashMap` contains `Integer` objects, Java can also translate certain reference-type variables into their original-type equivalent. For instance, Integer objects can be translated into int values, if needed. However, this can be misleading! If we try to translate a null reference into a number, we receive the *java.lang.reflect.InvocationTargetException* error. When we make use of this automatic translation, we have to be sure that the value we want to translate is not null. The above lastTwitch method must be fixed in the following way.

```java
public int lastTwitch(String name) {
    if(this.twitched.containsKey(name)) {
        return this.twitched.get(name);
    }

    return 0;
}
```

{% include_relative exercises/002.md %}
{% include_relative exercises/003.md %}
{: .exercises }
