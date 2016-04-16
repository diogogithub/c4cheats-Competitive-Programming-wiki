A `BigInteger` is a `Java` specific class that utilizes `String`s to create an Integer with no theoretical limits besides the amount of memory on the computer. The `BigInteger` is immutable meaning that the `.add()` method does not add to the object from which it is called, see below.

    BigInteger b = new BigInteger("5");

    b.add(BigInteger.ONE); // value of b is still 5
    b = b.add(BigInteger.ONE); // value of b is now 6


You can make a new `BigInteger` one of two ways, using a `String` or either an `int` or a `long`.

    BigInteger one = new BigInteger("5");
    BigInteger two = BigInteger.valueOf(5);
