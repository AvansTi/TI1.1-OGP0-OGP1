---
layout: ogp1
title: Abstract Classes
meta: Put extra info here, like if there any subjects required for this subject
todo: what should be improved in this chapter
---
{% include licence.md %}

## Abstract classes

In Exercise overwriting-methods-2 there's a problem though. It is possible to execute the following code

```java
Vector2D vector = new Vector3D(10,10,10);
```

This would not make any sense though, as a Vector3D would be the same as a Vector2D.

In the shape example of last chapter, there's also a big problem. It is possible in java to make a new `Shape`

```java
Shape shape = new Shape(Color.green);
```

This would of course be nonsense, as a 'shape' does not really have a surface area or circumference. The methods in this class now return 0, but we can also remove the code for these methods, by turning this class into an `abstract` class

```java
class Shape {
    private Color color;

    public Shape(Color color) {
        this.color = color;
    }
    public abstract double getArea();
    public abstract double getCircumference();
}
```

An abstract class can contain abstract methods, which are methods that do not have an implementation. There is no code for these methods because it makes no sense, like in our Shape example. This also makes sure that there can be no new Shape objects, because it has abstract methods. 

```java
Shape shape = new Shape(Color.green); // won't compile, as Shape is an abstract class
```

In order to make an object, just extend the Shape class, and implement the abstract methods, as done before. This new class is **not** abstract anymore.

<!-- TODO: abstract toString() -->

{% include_relative exercises/001.md %}
{% include_relative exercises/002.md %}
{: .exercises }
