---
layout: ogp1
title: Casting
meta: Put extra info here, like if there any subjects required for this subject
todo: what should be improved in this chapter
---
{% include licence.md %}

## Casting

We've seen casting before, where we had a double, but wanted to store it in a integer variable. We can also cast objects. In our previous example of the animals, a `Cow` is also an `Animal`, so we can store it, but not all `Animal`s are `Cow`s, so we can't store it that way. Let's look at an example

```java
Animal animal = new Cow(); // valid
Cow cow = (Cow)animal; // valid
Pig pig = (Pig)animal; // runtime exception
```

We can use casting on objects, but this casting is not always valid. If we try to cast a `Cow` object to a `Pig` object, java will give an error, as this is not supported behaviour.
Casting is only allowed to the right types, and to the sub or superclasses of an object. We can however, test if an object is an instance of a certain class.

- Casting to a superclass is called **upcasting**, and is always allowed, and is always done implicitly and automatically by java. This means you do not have to do any casting in `Animal animal = (Animal) new Cow()`, this is done automatically
- Casting to a subclass is called **downcasting**, and is **not** always allowed. For instance, a `Cow` object, stored in an `Animal` variable, can be casted to a `Cow`, but not to a `Pig`

If we want to perform downcasting, we need to check what the type of the object is. We can do this using the `instanceOf` operator

```java
Animal animal = new Cow();
if(animal instanceOf Cow) {
    System.out.println("This is a cow");
    Cow cow = (Cow)animal;
    //call specific cow method
} else if(animal instanceOf Pig) {
    System.out.println("This is a pig");
}
```

as you can see in this example, we could test every object to see what type it is, casting it, and then calling methods on that object. **This is however usually a sign of a bad design, and should be avoided as much as possible**. This is why there will be no exercises for casting
