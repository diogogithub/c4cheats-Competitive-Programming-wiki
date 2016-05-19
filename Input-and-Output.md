# Input and Output #
Programming contests require your program to be able to take in specified input data and output lines that correctly answer  the problem statement. Therefore, you must have a good understanding of how to succesfully implement an input parser class.
##Input Classes##
**Scanner Class:**
The `Scanner` is easy to use in order to obtain text from the Java console. In order to initialize a scanner you must construct it like so:

    Scanner scan = new Scanner(System.in); //Note that in this case "scan" is the name of the scanner. It could be anything else you choose.

The Scanner class has a variety of useful methods to get input. The most used of which are:

    //(Assuming our scanner is named scan)
    int n = scan.nextInt(); //Scans an integer

    String s = scan.next(); //Scans a string

    String s = scan.nextLine(); //Scans a string

The difference between these methods is that the first two (nextInt() and next()) both scan a segment of the text input that is separated by a space. nextLine() on the other hand, scans the entire line. If nextInt() is called until the input reaches the next line, calling nextLine() would return the first line which would be empty since all of the integers from that line were previously scanned. If, for example, we have integers in the first three lines, and an entire line we want to scan as a whole on the next line, we would have to call nextLine() three times after calling nextInt() three times, in order to be able to scan the fourth line. Alternatively, calling nextLine() four times and using the method `Integer.parseInt()` in order to receive an integer from the first three lines and also get the fourth line.

Other useful methods include:

    double d = scan.nextDouble();

    long n = scan.nextLong();

**BufferedReader Class:**
The BufferedReader is not as convenient as the Scanner class, but it has the advantage of being faster and using less memory. If the problem has a strict time limit, or only contains Strings, using a BufferedReader over a Scanner is strongly recommended. BufferedReaders are typically initialized like so:

    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

The best method to scan input with a BufferedReader is usually `br.readLine();`. This returns a string of the entire line, similar to `scan.nextLine();`. We can separate the line's spaces into Strings in two different ways.

The easiest and more convenient method is to use `String[] input = str.split(" ")`, where s is the name of the String. In this case, if String `str` was "The quick fox", input[0] would be "The", input[1] would be "quick", and input[2] would be "fox".

The faster and more efficient way to split a string is to use the StringTokenizer class. We could initialize a StringTokenizer and add each token to an ArrayList of strings to keep track of our input.

    StringTokenizer st = new StringTokenizer("The quick brown fox jumps over the lazy dog");
    ArrayList<String> input = new ArrayList<String>();
    while(st.hasMoreTokens()){
        input.add(st.nextToken());
    }

This code would succesfully add every single word in the sentence into the ArrayList in the correct order, and is useful for problems that require very efficient I/O.
##Output##