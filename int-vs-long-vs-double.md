Before we start talking about the difference between the types, lets talk about why they are the same.   All three types are primitive data types.  So they are able to be declared without a constructor.   However, they do have what we call wrapper classes.   A wrapper class name will be the full name of the type.  For example, `int` would be `Integer`, `double` would be `Double` and `long` would be `Long`.   There are some pretty cool things that you can do within those wrapper classes, such as conversions. 

**int**

The `int` is the most basic data type in java and probably the one everyone is familiar with. The `int` is short for `Integer` (a class which can wrap the primitive `int`). The `int` data type has a range from -2147483648 to 2147483647. `int`s are all whole real numbers. You cannot have a decimal if you have an `int`. If you were to divide two numbers that are not evenly divisible say 10 and 3, the result you would get would be 3.

_Important Variables/Methods_
* `Integer.MAX_VALUE` value is 2147483647
* `Integer.MIN_VALUE` value is -2147483647
* `Integer.SIZE` values is the number of bits required to store the number.
* `Integer.bitCount(int n)` will return an int that will be the number of 1s in the binary representation. 
* `Integer.highestOneBit(int n)` will return the position of the highest 1 in the binary representation.


**long**

The `long` (wrapper class `Long`) is, in basic terms very similar to the `int`. Both only contain whole real numbers. If you were to divide 10l / 3l the result would be 3l. Unlike an `int` though the `long` can store much larger numbers. The maximum value of a `long` is 9223372036854775807 and the minimum value is -9223372036854775808. 

**double**

The `double` (wrapper class `Double`) is where the 3 start to diverge a little. The `double` unlike both an `int` and a `long` can store decimals. If you were to divide 10.0 / 3.0 the result would be 3.333333333333333. Both the `double` and `long` are 64 bit numbers. The `double` has a minimum value of 4.9E-324 and a maximum value of 1.7976931348623157E308.
