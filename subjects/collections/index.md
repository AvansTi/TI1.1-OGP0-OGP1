---
layout: ogp1
title: Collections
meta:
todo: 
---
{% include licence.md %}

## Collections

The class library [Collections](http://java.sun.com/javase/8/docs/api/java/util/Collections.html) is Java's general-purpose library for collection classes. As we can see, Collections provides methods to sort objects either through the interface `Comparable` or `Comparator`. In addition to sorting, we can use this class library to retrieve the minimum and maximum values (through the methods `min` and `max`, respectively), retrieve a specific value (`binarySearch` method), or reverse the list (`reverse` method).

### Search

The `Collections` class library provides a pre-made binary search functionality. The method `binarySearch()` returns the index of our searched key, if this is found. If the key is not found, the search algorithm returns a negative value. The method `binarySearch()` makes use of the interface `Comparable` to retieve objects. If the object's method `compareTo()` returns the value 0, i.e. if it is the same object, the key is considered found.

Our class `ClubMember` compares people's heights in its method `compareTo()`, i.e. we look for club members whose height is the same while we parse our list.

```java
List<ClubMember> clubMembers = new ArrayList<ClubMember>();
clubMembers.add(new ClubMember("mikael", 182));
clubMembers.add(new ClubMember("matti", 187));
clubMembers.add(new ClubMember("joel", 184));

Collections.sort(clubMembers);

ClubMember wanted = new ClubMember("Name", 180);
int index = Collections.binarySearch(clubMembers, wanted);
if (index >= 0) {
    System.out.println("A person who is 180 centimeters tall was found at index " + index);
    System.out.println("name: " + clubMembers.get(index).getName());
}

wanted = new ClubMember("Name", 187);
index = Collections.binarySearch(clubMembers, wanted);
if (index >= 0) {
    System.out.println("A person who is 187 centimeters tall was found at index " + index);
    System.out.println("name: " + clubMembers.get(index).getName());
}
```

The print output is the following:

```output
A person who is 187 centimeters tall was found at index 2
name: matti
```

Notice that we also called the method `Collections.sort()`, in our example. This is because binary search cannot be done if our table or list are not already sorted up.
