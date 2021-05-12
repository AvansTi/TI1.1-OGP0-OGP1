---
layout: default
title: Bit operations
meta:
todo: 
---
{% include licence.md %}

## Bit operators

So far we've been calculating with numbers using the `+`, `-`, `/`, `%` and `*` operators. These operations match with the normal math that we're used to. For computer programming however, there are also some other operations that operate on a bit level.

Internally, all numbers in the computer are represented using a binary format. So for instance the code

```java
int months = 12;
```

will store the number 12 in the memory of the computer. It is not stored as `12`, but more as `1100`. When it is printed out with `System.out.println` however, it is converted back to the decimal format, for human viewing. An explaination on the binary system is beyond the scope of this course, but the concept can be found on [wikipedia](https://en.wikipedia.org/wiki/Binary_number) or [other](https://learn.sparkfun.com/tutorials/binary) [sources](https://www.youtube.com/watch?v=LpuPe81bc2w). In java, by default, numbers are written in base 10. In the example above, `12` is the number 12 in base 10. Java supports other based numbers, by adding a prefix to the number.

```java
int decimalMonths = 12;        //base 10
int binaryMonths = 0b1100;     //base 2, binary
int octalMonths = 014;         //base 8, octal
int hexMonths = 0xC;           //base 16, hexadecimal
```

these variables will all contain the number 12. In order to view the binary representation of a number, we can use the helper method `Integer.toBinaryString()`

```java
System.out.println(Integer.toBinaryString(12));
```

```output
1100
```

These bits have an order. There are 2 ways of storing these bits in memory. The bit representing `1` is the **Least Significant Bit**, and the bit representing the largest value (128 in an 8-bit number for instance) is the **Most Significant Bit**. These way these values are stored in memory is called the [Endianness](https://en.wikipedia.org/wiki/Endianness), and is not the same on all computersystems. Java uses **Big Endian**, meaning the bit on the end is the most significant bit. This is only important on the way memory is stored, and won't affect us as a programmer.

Besides writing down numbers in different number systems, there are also a number of interesting operations we can do on these numbers

### Bitwise And operator

The bitwise And operator in java is written using the `&` operator. A bitwise And will combine the bits of 2 numbers with the And operator. An example

```java
int firstNumber =  0b1010;
int secondNumber = 0b1100;
int result = firstNumber & secondNumber;
System.out.println(Integer.toBinaryString(result));
```

```output
1000
```

As we can observe, the only bits set to 1 in the result are the ones where the bit is set to 1 both in the `firstNumber` and the `secondNumber`. This can be combined in this small table

| first | second | result |
|-------|--------|--------|
| 0     | 0      | 0      |
| 1     | 0      | 0      |
| 0     | 1      | 0      |
| 1     | 1      | 1      |

### Bitwise Or operator

The bitwise Or operator in java is written using the `|` operator. A bitwise And will combine the bits of 2 numbers with the Or operator. An example

```java
int firstNumber =  0b1010;
int secondNumber = 0b1100;
int result = firstNumber | secondNumber;
System.out.println(Integer.toBinaryString(result));
```

```output
1110
```

As we can observe, the bits set to 1 in the result are the ones where the bit is set to 1 either one of the `firstNumber` and the `secondNumber`. This can be combined in this small table

| first | second | result |
|-------|--------|--------|
| 0     | 0      | 0      |
| 1     | 0      | 1      |
| 0     | 1      | 1      |
| 1     | 1      | 1      |

### Bitwise Xor operator

The bitwise Xor operator, or Exclusive Or, in java is written using the `^` operator. A bitwise Xor will combine the bits of 2 numbers with the Xor operator. An example

```java
int firstNumber =  0b1010;
int secondNumber = 0b1100;
int result = firstNumber ^ secondNumber;
System.out.println(Integer.toBinaryString(result));
```

```output
0110
```

As we can observe, the bits set to 1 in the result are the ones where only one bit is set to 1 either one of the `firstNumber` and the `secondNumber`. This can be combined in this small table

| first | second | result |
|-------|--------|--------|
| 0     | 0      | 0      |
| 1     | 0      | 1      |
| 0     | 1      | 1      |
| 1     | 1      | 0      |


### Representation of negative numbers: Two's complement

So far we've only worked with positive numbers, but how do we store negative numbers? A first thought would be to reserve a single bit for the sign. If the on the most left is 1, it is a negative number, if it is a 0, it is a positive number. So for an 8bit number, we could do

```java
byte a = 0b00000001;    // 1
byte b = 0b10000001;    // -1
byte c = 0b00000000;    // 0
byte d = 0b10000000;    // -0?????
```

This leads to some problems though. For one, there is the problem of a double representation for 0. It also represents some challenges for computers to compute. [Two's complement](https://en.wikipedia.org/wiki/Two's_complement) is another system that was suggested back in 1945. In two's complement, there is only one representation of 0 (`0b00000000`) and it has some other additional advantages.

In Two's complement, the most significant bit is used to indicate a negative number, and all other bits are flipped (the complement), with one added. This can be seen in the following table, for 3-bit numbers. 3 bits range from -4 to 3.

| Decimal | Binary |
|---------|--------|
| 0       | 0`00`  |
| 1       | 0`01`  |
| 2       | 0`10`  |
| 3       | 0`11`  |
| -4      | 1`00`  |
| -3      | 1`01`  |
| -2      | 1`10`  |
| -1      | 1`11`  |

As seen in the table, for positive numbers, there's nothing special. For negative number, the MSB is set to 1, and the number is represented as the flipped bits, plus 1. For instance for `-4`, the bits are set to `00`. flipped around this is `11` or 3, and then with 1 added, makes 4. Expanding this to the 8-bit range, we can make the following table

| Decimal | Binary    |
|---------|-----------|
| 0       | 0000 0000 |
| 1       | 0000 0001 |
| 2       | 0000 0010 |
| 126     | 0111 1110 |
| 127     | 0111 1111 |
| −128    | 1000 0000 |
| −127    | 1000 0001 |
| −126    | 1000 0010 |
| −2      | 1111 1110 |
| −1      | 1111 1111 |

Compared to other systems for representing signed numbers, two's-complement has the advantage that the fundamental arithmetic operations of addition, subtraction, and multiplication are identical to those for unsigned binary numbers, making it easier and faster to implement

### Bitshift Operators

Another operator often used for bit operations is bit shifting. Bit shifting is moving all the bits and shifting them a number of bits to the left or right. Bit shifting is done by the `<<` or `>>` operators. The `<<` operator shifts all bits left, and the `>>` shifts all bits right. 

```java
int a = 0b00000001 << 5;            // a = 0b00100000
int b = 0b10000000 >> 7;            // b = 0b00000001

while(a != 0) {
    System.out.println(a);
    a = a >> 1;                     // will keep shifting the bits in a to the right
}
```

When shifting bits, the 'new' bits inserted are always 0. In result, shifting 1 to the right has the effect of dividing by 2, while shifting 1 to the left has the effect of multiplying by 2 (or even better, $$x >> n = x / 2^n$$ and $$x << n = x * 2^n$$). 

The bitshift operators will ignore the sign-bit, resulting in the same behaviour for negative numbers. There is also a third bitshift operator in java, the *unsigned right shift* `>>>` operator, which will shift including the signbit

```java
int a = -1 >> 1;                    // -1 will shift to -2
int b = -1 >>> 1;                   // -1 will shift to 2147483647
```

### Not Operator
The not operator flips all bits in a number, including the sign bit.

```java
int a = ~1;                         //~1 = -2
int b = ~0;                         //~0 = -1
```

### Practical applications

#### Bits as a boolean array

An integer is made up of 32 bits, which can all be individually set. This can be used to store multiple true/false values. In a single int, we can store 32 booleans, which is a lot smaller to communicate (smaller filesize, less network data usage). To access these booleans, we can make a method to test if a bit is set, and a method to set or unset a bit

```java
public static boolean isBitSet(int number, int bit) {
    return ((number >> bit) & 1) != 0;
}
```

This method will bitshift the number to the right, so the bit we're interested in, is in the most-right position. After this all other bits are 'removed' by doing an and operation on the last bit. Another way to implement this would be to change the and mask with the right bit set. This can be done with the following code

```java
public static boolean isBitSet(int number, int bit) {
    return (number & (1 << bit)) != 0;
}
```

These two methods are doing the same thing (though work differently)

To set a bit, we can combine the right bitmask with an or operation, and to unset a bit, we can use an and operation with a mask with most values set to 1

```java
public static int setBit(int number, int bit) {
    return number | (1<<bit);
}
public static int clearBit(int number, int bit) {
    return number & ~(1<<bit);
}
```

This is a function often used in programming, where a large number of related booleans have to be passed to a method as parameter.

```java
int HALIGN_LEFT =   1<<0;
int HALIGN_CENTER = 1<<1;
int HALIGN_RIGHT =  1<<2;
int VALIGN_TOP =    1<<3;
int VALIGN_CENTER = 1<<4;
int VALIGN_BOTTOM = 1<<5;

public static void printText(String text, int alignment) {
    if(alignment & HALIGN_LEFT != 0) {
//      ...
    }
}

printText("Hello World", HALIGN_CENTER | VALIGN_BOTTOM);
```

#### Combining numbers

An integer is 32bit in size. This means we can store a single number in it, with 4 294 967 296 different options. In some low-level applications, it's only possible to send a single parameter, where we want to send more than 1 parameter. In this case, we can *encode* 2 numbers into a single number. We can do this in the decimal system as well. Suppose we can only send a 6-digit number, but we want to send 2 smaller numbers. We could just stick these 2 numbers together. The number `123456` would mean `123` and `456`, and `001002` would mean `1` and `2`. We can use some modulo arithmatic to seperate these numbers (`int number1 = number % 1000; int number2 = number / 1000`)

This principle also works with binary numbers. Suppose we'd like to encode 2 8-bit numbers into a single 16-bit number. It's easy to just stick them together

```java
int a = 0b10101010;
int b = 0b01010101;
int combined = a<<8 | b<<0;     // combined is 0b1010101001010101
```

By bitshifting the first number left, and combining both numbers with the `Or` operator, the numbers become one long number. This is of course limited to the size of the variable. Bitshifting is also used to read out these numbers again



{% include_relative exercises/001.md %}
{% include_relative exercises/002.md %}
{: .exercises }



