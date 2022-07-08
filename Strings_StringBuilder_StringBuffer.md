## 1. What will appear in the console as a result of the program fragment?

    String a = "java";
    a.toUpperCase();
    System.out.println(a);

"java". String toUpperCase() returns a copy of the string. The intermediate result String a.toUpperCase() is not stored 
anywhere, therefore in the output we get a string from the variable a = "java"

## 2  What will appear in the console as a result of the program fragment?

    String s1 = "Java";
    String s2 = "Java";
    String s3 = new String("Java");
    System.out.println("s1 == s2 : " + (s1 == s2));
    System.out.println("s1 == s3 : " + (s1 == s3));
    System.out.println(s1.equals(s3));

------

    s1 == s2 : true
    s1 == s3 : false
    true

When creating an instance of the String class by assigning its reference to a literal, the latter is placed in the so-called "pool of literals". If in the future another reference to a literal equivalent to the previously declared one is created, an attempt will be made to add it to the "pool of literals". Since an identical literal already exists there, a duplicate cannot be placed, and the second link will be to an existing literal.
Since in Java all references are stored on the stack, and objects are stored on the heap, when creating an s2 object, a reference is first created, and then an object is set to correspond to this reference. In this situation, s2 is associated with an already existing literal, since the object s1 has already made a reference to this literal. When s3 is created, the constructor is called, i.e. memory allocation occurs before initialization, and in this case a new object is created in the heap.
The equals method returns true if the argument is a String object that represents the same sequence of characters as this object.
## 3 Is it possible to inherit from the String class?

This class is final, which means that you cannot inherit this class.

## 4 Name the main, in your opinion, methods of the String class.
● String concat(String s) or "+" — merge strings;
● boolean equals(Object ob) and equalsIgnoreCase(String s) — comparing case-sensitive and case-insensitive strings, respectively;
● int compareTo(String s) and compareToIgnoreCase(String s) — lexicographic comparison of strings, case-sensitive and case-insensitive. The method subtracts the codes of the first different characters of the calling and transmitted string into the string method and returns an integer value. The method returns the value zero in the case when equals() returns the value true;
● boolean contentEquals(StringBuffer ob) — comparison of a string and the contents of an object of type StringBuffer;
● String substring(int n, int m) — extract a substring of length m-n from a string, starting from position n. The numbering of characters in a string starts from zero;
● String substring(int n) — extract a substring from a string starting from position n;
● int length() — determining the length of the string;
● int indexOf(char ch) — determining the position of a character in a string;
● static String valueOf(value) — conversion of a base type variable to a string;
● String toUpperCase()/toLowerCase() — convert all characters of the calling string to uppercase/lowercase;
● String replace(char c1, char c2) — replacing all occurrences of the first character in the string with the second character;
● String intern() — puts a string in the "pool" of literals and returns its object reference;
● String trim() — removes all spaces at the beginning and end of the string;
● char charAt(int position) — returning a character from the specified position (numbering from zero);
● boolean isEmpty() — returns true if the string length is 0;
● char[] GetChars(int srcBegin, int srcEnd, char[] dst, int dstBegin) — extracting string characters into an array of characters;
● static String format(String format, Object... args), format(Locale l, String format, Object... args) — generates a formatted string obtained using the format, internationalization, etc.;
● String[] split(String regex), String[] split(String regex, int limit) — searching for the occurrence of a given regular expression (separator) in a string and dividing the source string accordingly into an array of strings.

## 5 What kinds of constructors does the String class use?
The String class supports several constructors, for example: String(), String(String str), String(byte[] ascii char), String(char[] unicodechar), String(StringBuffer sbuf), String(StringBuilder sbuild), etc. These constructors are used to create objects of the String class based on initialization with values from an array of type char, byte, etc.
## 6 Which classes in the Java standard library work with strings?
The StringBuilder and StringBuffer classes are "twins" and are close to the String class in their purpose, but unlike the latter, the contents and sizes of objects of the StringBuilder and StringBuffer classes can be changed. Also classes: Pattern, Matcher, PatternSyntaxException.
## 7 Why are instances of the String class in Java immutable and finalized?
The main reasons for String immutability in Java are security and the presence of a String pool.
● you can pass a string between threads without fear that it will be changed
● there are no problems with synchronization of streams
● No memory leak problems
● no access and security issues when using strings to pass authorization parameters, open files, etc.
● hashcode caching
● Memory savings when using a row pool to store duplicate rows.
## 8 What is the difference and what do StringBuffer and StringBuilder have in common?
The main difference between StringBuilder and StringBuffer is the thread safety of the latter. The higher processing speed is a consequence of the lack of thread safety of the StringBuilder class. The StringBuilder and StringBuffer classes are "twins" and are close to the String class in their purpose, but unlike the latter, the contents and sizes of objects of the StringBuilder and StringBuffer classes can be changed.
## 9 When is it better to use StringBuffer, and when is StringBuilder?
StringBuilder should be used if there is no possibility of using the object in competing threads.
## 10 What methods are available in the StringBuffer and StringBuilder classes that are not present in the String class?
● void SetLength(int n) — setting the buffer size;
● void ensureCapacity(int minimum) — setting a guaranteed minimum buffer size;
● int capacity() — returns the current buffer size;
● StringBuffer append(parameters) — adding an argument to the contents of the string representation object, which can be a symbol, a base type value, an array, and a string;
● StringBuffer insert(parameters) — inserting a character, object, or string into the specified position;
● StringBuffer deleteCharAt(int index) — deleting a character;
● StringBuffer delete(int start, int end) — deleting a substring;
● StringBuffer reverse() — reversal of the object contents.
## 11 Using the functions of string classes, write a fragment of a program that will determine whether a string is a palindrome.
    public static Boolean isPalindrome(String str) {
    return str.equals((new StringBuilder(str)).reverse().toString());
    }
## 12 How can Java strings be concatenated?
● String concat(String s) or "+" — merge strings;
● static String format(String format, Object... args), format(Locale l, String format, Object... args) — generates a formatted string obtained using format, internationalization, etc.;
● StringBuffer append(parameters) — adding a string representation of an argument to the contents of the object, which can be a symbol, a value base type, array and string;
● StringBuffer insert(parameters) — insert a character, object, or string into the specified position;
● using the "+" operator, the append() method of the StringBuilder class is implicitly used;
° using the join() method which combines the first lines leaving a separator between them (also passed as a method argument).
## 13 What is the difference between empty and null strings?
An empty string (for example "") means that a string constant was created in the string pool as part of the declaration of a string variable, and a certain amount of memory was allocated for it. The null string has no memory allocated for it.
## 14 In what encoding are the characters stored in the string?
Unicode UTF-16BE encoding
## 15 What interfaces do the String, StringBuffer and StringBuilder classes implement?
The String class implements the Serializable, Comparable, and CharSequence interfaces. The StringBuilder and StringBuffer classes implement the Serializable, Appendable, and CharSequence interfaces.
## 16 What are code points and code units?
This is the number that identifies the symbol. Two well-known standards for assigning numbers to characters are ASCII and Unicode. When you're trying to use an encoding that uses fewer bits per character than is required to represent all possible values (like UTF-16, which uses 16 bits), you need some workaround. Thus, Surrogates are 16-bit values that indicate characters that do not fit into a single two-byte value. Java uses UTF-16. In particular, the char (symbol) is a two-digit unsigned value that contains a UTF-16 value.
## 17 Explain the purpose of the intern() method. What will appear in the console as a result of the program fragment?
    class GFG {
    public static void main(String[] args) {
    String s1 = new String("GFG");
    String s2 = s1.intern();
    System.out.println(s1 == s2);
    System.out.println(s1.equals(s2));
    String s3 = "GFG";
    System.out.println(s2 == s3);
    }
    }
____
    false
    true
    true
● the intern() method puts a string in the "pool" of literals and returns its object reference. Since this method was called for the variable s1, the result of s1 == s2 is false, because variables have different references.
° the result of the s1.equals(s2) method is true, because these strings are equivalent.
° result of work s2 == s3 true because when s3 was created, the last reference to "GFG" obtained by the intern() method was taken from the pool when the variable s2 was set.
## 18 What method in the String class can be used to check a string for compliance with a regular expression?
The matches() method - accepts a regular expression and returns true if the string matches this expression. Otherwise returns false.
## 19 What is a regular expression?
## What classes are the regex capabilities of the Java language based on?
### In which package are these classes located?
● Regular expressions are a formal language for searching and manipulating substrings in the text, based on the use of metacharacters (wildcard characters). A pattern string is used for the search (English pattern, in Russian it is often called a "template", "mask"), consisting of symbols and metacharacters and specifying the search rule.
● java.util.regex class.Pattern is used to define regular expressions (templates) for which a match is being searched in a string, file, or other object representing a sequence of characters. Special syntactic constructions are used to define the template. You can get information about each compliance using the java.util.regex class.Matcher.
## 20 Which of the ways to compare strings is preferable?
## str.equals("abc");
## or
## "abc".equals(str);
The second method is preferable. Before comparing str.equals("abc"), it would be correct to compare str with null, so as not to get a NullPointerException. I.e., the construction of str will be correct!= null && str.equals("abc"). When implementing such a method "abc".equals(str), checking for null in this case is not necessary.