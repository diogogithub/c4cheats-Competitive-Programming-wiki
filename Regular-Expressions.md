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