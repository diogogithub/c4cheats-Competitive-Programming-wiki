`Regular Expression` (Regex) is a powerful tool used to find and manipulate patterns in a string of text. It is used in many programming languages, including (naturally) Java.

Here are some examples where Regex can be useful:
* To determine if a string is a number: `[0-9]+`
* To count all the vowels in a string:  `[aeiou]`
* To check if a string contains only one distinct character: `(.)\\1*`
* To check if a String is a valid 10-digit phone number:  
`((\\(\\d{3}\\))|(\\d{3}))\\s?-?\\s?\\d{3}-\\d{4}`


Some methods in the Java String class that use Regex:
* `String.matches(String regex)`
* `String.split(String regex)`
* `String.replaceAll(String regex, String replacement)`
* `String.replaceFirst(String regex, String replacement)`

###The Basics
The simplest thing to do with regex is to match a String. Let's say we have a String called `str`. If we wanted to see if the value of the string was "pickles", we would typically use the `.equals` method. For example:  


    if (str.equals("pickles"))
        System.out.println("Yes");
    else
        System.out.println("No");

The way to do this with regex is very similar. But instead of using `.equals`, use **.matches**:

    if (str.matches("pickles"))
        System.out.println("Yayyy!!");


Note that the .matches method doesn't always work like the .equals method. In fact, there are many more things that can be done with the regex method. But before we go into that, it's important to know the escape characters in regex. These are characters which must be escaped with the `\` character (`\\` in a java string), or else they will be interpreted with a different meaning. The following characters must be escaped to retain their literal meaning: `()[]{}\^.$|?*+`
As we will see later, there are exceptions to this rule.

#####Examples
| String | Regex | String.matches(Regex) |
| ---- | ---- | ---- |
| "Hello" | "Hello" | true |
| "$100" | "$100" | false |
| "$100" | "\\\\$100" | true |
| "Why?" | "Why?" | false |
| "Why?" | "Why\\\\?" | true |
| "2+3" | "2+3" | false |
| "2+3" | "2\\\\+3" | true |


###Square Brackets and Character Ranges
A very useful feature of regex is the ability to check whether a character is part of a specific set of characters. This is done by placing all the possible characters inside of square brackets. For example, the regex `"[aeiou]"` will match the string `"a"`, as well as `"e"`, `"i"`, `"o"`, and `"u"`. It will not match anything else. Almost any character can be placed inside of the brackets, including most of characters that usually need to be escaped.

Let's say we wanted to use regex to check whether a 2-digit number is divisible by 10. We can use `"[0123456789]0"`. There are 2 parts to this regex: the numbers inside of the bracket, and 0. Since the bracket part can match any single numeric digit, the whole regex string can match `"10"`, `"20"`, ..., `"90"`, but also `"00"`. To avoid this, just change it to `"[123456789]0"`.

You may be thinking that this is a lot of typing for something so simple. Why type `"[abcdefghijklmnopqrstuvwxyz]"` to match a letter when you can just use `Character.isLowerCase(ch)` or `'a' <= ch && ch <= 'z"`? The way around this is to use a range: `"[a-z]"` to match a lower-case letter, `"[A-Z]"` to match an upper-case letter, or `"[0-9]"` to match a digit. If you wanted to check part of the alphabet, you could use `"[m-z]"`. You can also combine them: `"[a-df-z1-9]"` will match any lower-case letter other than 'e' or any non-zero digit. It's important to note that while it is legal to change around the order of letters/numbers, you CANNOT change the order of the range, i.e. use `"[z-a]"` or `"[9-0]"`. This will result in an Exception.