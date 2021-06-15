---
layout: default
title: Searching
meta: Put extra info here, like if there any subjects required for this subject
todo: what should be improved in this chapter
---
{% include licence.md %}

## Searching

In addition to sorting, another very typical problem that a programmer runs into is finding a certain value in an array. Earlier, we've implemented methods that search for values in lists and arrays. In the case of arrays, values and strings can be searched for in the following way:

```java
public static boolean isInArray(int[] array, int searchingFor) {
    for ( int value : array ) {
       if ( value == searchingFor )  {
           return true;
       }
    }

    return false;
}

public static boolean isWordInArray(String[] array, String searchingFor) {
    for ( String word: array ) {
        if ( word.equals(searchingFor) )  {
            return true;
        }
    }

    return false;
}
```

An implementation like this is the best we've been able to do so far. The downside of the method is that, if the array has a very large amount of values in it, the search will take a lot of time. In the worst case scenario the method goes through every single cell in the array. This means that going through an array that has 16777216 cells does 16777216 cell inspections.

On the other hand, if the values in an array are ordered by size, the search can be done in a notably faster way by applying a technique called binary search. Let's investigate the idea of binary search with this array:

```output
// indexes   0   1   2   3    4   5    6   7   8   9  10
// values   -7  -3   3   7   11  15   17  21  24  28  30
```

Let's assume that we want to find the value 17. Let's utilize the information that the values of the array are in order instead of going through the array from the beginning. Let's inspect the middle cell of the array. The middle cell is 5 (the largest index 10 divided by two). The middle cell is marked with the asterisk:

```output
                                  *
// indexes   0   1   2   3    4   5    6   7   8   9  10
// values   -7  -3   3   7   11  15   17  21  24  28  30
```

At the middle is the value 15, which was not the value we were looking for. We're looking for the value 17, so since the cells of the array are ordered by size, the value cannot be on the left side of the 15. So we can determine that all indexes that are smaller or equal to 5 do not have the value we are looking for.

The area where we are searching for the value we want to find can now be limited to values that are on the right side of the index 5, or in other words, in the indexes [6, 10] (6, 7, 8, 9, 10). In the following, the searched value cannot be in the part of the array which is red:

```output
// indexes    ~~0   1   2   3   4    5~~    6    7   8   9  10
// values    ~~-7  -3   3   7  11   15~~   17   21  24  28  30
```

Next, let's inspect the middle index of the area that we have left; the middle index of indexes 6-10. The middle index can be found by getting the sum of the smallest and largest index and dividing it by two: (6+10)/2 = 16/2 = 8. The index 8 is marked with the asterisk below.

```output
                                                *
// indexes    ~~0   1   2   3   4    5~~    6   7   8   9   10
// values    ~~-7  -3   3   7  11   15~~   17   21  24  28  30
```

In index 8, we have the value 24, which was not the value we were looking for. Because the values in the array are ordered by size, the value we are searching for can not, in any case, be on the right side of the value 24. We can deduce that all indexes that are larger or equal to 8 can not contain the value we are looking for. The search area gets narrowed down again, the grey areas have been dealt with:

```output
// indexes    ~~0   1   2   3   4    5~~    6   7   ~~8   9   10~~
// values    ~~-7  -3   3   7  11   15~~   17   21  ~~24  28  30~~
```

The search continues. Let's inspect the middle index of the area that we have left to search, that is, the middle index of indexes 6-7. The middle index can again be found out by getting the sum of the smallest and largest index of the search area and then dividing it by two: (6+7)/2 = 6.5, which is rounded down to 6. The spot has been marked with the asterisk.

```output
                                          *
// indexes    ~~0   1   2   3   4    5~~    6    7   ~~8   9  10~~
// values    ~~-7  -3   3   7  11   15~~   17   21  ~~24  28  30~~
```

In the index 6 we have the value 17, which is the same as the value we've been looking for. We can stop the search and report that the value we searched for is in the array. If the value wouldn't have been in the array - for example if the searched-for value would've been 16 - the search area would have eventually been reduced to nothing.

```output
                                          *
// indexes    ~~0   1   2   3   4    5~~    6   7   ~~8   9   10~~
// values    ~~-7  -3   3   7  11    15~~   17  21  ~~24  28  30~~
```

So for the idea of binary search to become clear to you, simulate with pen and paper how the binary search works when the array is the one below and first you're searching for value 33 and then value 1.

```output
// indexes   0   1   2   3   4   5   6   7   8   9  10  11  12  13
// values   -5  -2   3   5   8  11  14  20  22  26  29  33  38  41
```

With the help of binary search we look for cells by always halving the inspected area. This enables us to search in a very efficient way. For example, an array of size 16 can be divided in half up to 4 times, so 16 -> 8 -> 4 -> 2 -> 1. On the other hand, an array that has 16777216 cells can be halved up to 24 times. This means that with binary search we only need to inspect up to 24 cells in an array that has 16777216 cells in order to find our desired cell.

*The efficiency of binary search can be inspected with logarithms. A base two logarithm ($$log_2$$) of the number 16777216 is 24 -- with the base two logarithm we can calculate how many times a number can be halved. Respectively the base two logarithm of the number 4294967296 ($$log_2 4294967296$$) is 32. This means that searching from a sorted array of 4294967296 different values would only take up to 32 cell inspections. Efficiency is an essential part of computer science.*

{% include_relative exercises/001.md %}
{% include_relative exercises/002.md %}
{: .exercises }
