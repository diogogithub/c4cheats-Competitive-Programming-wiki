**String basics:**
A `String` is a collection of characters or `char`s. Since `String` starts with a capital 'S' we can tell it is a class meaning it will have methods. In Java `String`s can be declared one of two ways.

    String one = "Hello World";
    String two = new String("Hello World"); // these lines do the same thing

**String Concatenation:**
`String`s like primitive data types such as `int` can be added together. Though unlike something like an `int` it is not possible to subtract `String`s. `String` concatenation refers to the process of adding two `String`s using the '+' symbol. An example is below.

    String a = "This is" + " an example"; // the String a would read "This is an example"
    String b = a + " " + "of concatenation"; // String b would read "This is an example of concatenation"

**Finding all characters in a string:**
To find a character in a string, we must use the `s.charAt(n)` method where "s" is the name of the string and "n" is the position of the `char`. The position of the first `char` is at 0, while the last char would be at `s.length()-1`. The method `s.length()` returns the `int` value of the number of characters in a `String`.

    String s = "Hello World";
    for (int i = 0; i < s.length(); i++) {
        System.out.println(s.charAt(i)); // this will print every character of the string on a different line.
    }

**Generating all possible substrings:**
We will use a double `for` loop, the outer loops through all the possible starting positions of substrings and the inner generates all lengths for a substring starting at the position in the outer loop. The code below generates all possible substring, to make use of them add them to an `array` after they are created or place an `if` statement below them.

    String test = "Hello World";
    for (int o = 0; o < test.length(); o++) {
        for (int i = 1; i+o < test.length(); i++) {
            String sub = test.substring(o,i+o);
        }
    }

