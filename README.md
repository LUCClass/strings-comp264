# COMP 264 Strings Assignment

Your job in this homework assignment is to write a couple of functions that perform operations on strings. As we talked about in class, strings are large objects that cannot fit in a single register. Standard operations that we can do on ints and floats like compare and copy don't make sense for strings. High-level languages like Java have built-in support for string operations, but under the hood those operations are implemented in functions that treat the string as a data structure. In this homework assignment, you will be writing those functions yourself in assembly language. The specific tasks are below:

1. Write a function called `string_legnth` that computes the length of a NULL-terminated string. The input to this function will be a pointer to a string passed in R0. The output of the function will be the string's length in bytes, returned in R0.
2. Write a function called `string_copy` that copies a NULL-terminated string from one place in memory to another. The inputs to this function will be a pointer to the source string in R0 and a pointer to the destination in R1.


## Details

## ASCII

Characters--the building blocks of strings--are stored in computers in a code called ASCII. Each symbol in the latin alphabet is assigned an integer value between 1-127 so that each character can be stored in one byte of memory. See the [ASCII table](http://www.asciitable.com) for the specific assignments of characters to integers.

### Thinking about strings as data structures

Strings in C and assembly language are implemented as arrays that can have a variable length. The length of the string is not explicitly encoded anywhere--there is no String.length property or method that can easily tell us the length of a string. Instead, strings have a special NULL terminator to mark the end of the string. The NULL terminator is a single byte that has the special value 0, which does not code for any printable characters in ASCII. For example, the string "NEIL" is shown below coded as a NULL-terminated ASCII string.


|    Character    | ASCII |
|-----------------|-------|
|        N        | 0x4E  |
|        E        | 0x45  |
|        I        | 0x49  |
|        L        | 0x4C  |
| NULL TERMINATOR | 0x00  |

The string "NEIL" is 5 bytes long (including the NULL terminator at the end), so it will not fit into a 32-bit (4-byte) register. We can only tell how long the string is by counting the number of bytes starting at the beginning up to (and including) the NULL terminator. Consider the snippet of Java code below:


    public class Test {
      public static void main(String args[]) {
        String Str1 = new String("NEIL");
        String Str2 = Str1;

        System.out.print(Str2);
        }
    }

In this snippet, we are creating a string `Str1` and initializing it. We then create a second string `Str2` and *copy* the first string's value to the second string.




