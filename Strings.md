**Generating all possible substrings:**
We will use a double `for` loop, the outer loops through all the possible starting positions of substrings and the inner generates all lengths for a substring starting at the position in the outer loop. The code below generates all possible substring, to make use of them add them to an `array` after they are created or place an `if` statement below them.

    String test = "Hello World";
    for (int o = 0; o < test.length(); o++) {
        for (int i = 1; i+o < test.length(); i++) {
            String sub = test.substring(o,i+o);
        }
    }