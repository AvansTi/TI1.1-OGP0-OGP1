---
layout: default
title: For loop
meta: 
todo: 
---
{% include licence.md %}

## For loops

By now you will have noticed that there are usually 3 important components in a loop; the initialization, condition and increment

```java
int i = 0;              //initialization
while(i < 10) {         //condition
    System.out.println(i);
    i++;                //increment
}
```
{: .interactive .hideStack #for-1 }

These 3 parts are key to a successful loop, and for instance, forgetting the increment will result in an infinite loop. They are split up on 3 different lines, which is not good for the structure of your code. To improve the structure, java offers a for-loop. This for-loop combines these 3 parts in a single line

```java
for(int i = 0; i < 10; i++) {
    System.out.println(i);
}
```
{: .interactive .hideStack #for-2 }

This program is identical to the while loop. The for has all 3 different components between brackets, and is therefore different than the while() or if() conditions. This `for`-syntax is very powerful, but can some time getting used to. For now, you can pick if you do loops with a while() statement or a for() statement


{: .exercises }
