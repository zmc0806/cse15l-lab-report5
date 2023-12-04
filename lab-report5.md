## Part 1 – Debugging Scenario

Question 

![image](https://raw.githubusercontent.com/zmc0806/cse15l-lab-report5/main/problem.jpeg)


![image](https://raw.githubusercontent.com/zmc0806/cse15l-lab-report5/main/ed.jpeg)


TA: Alright, I understand your issue. You need to ensure that JUnit is aware of which specific file to test within your bash script.You should adjusting the last line of your bash.

Student: Got it, that makes sense. I've updated the bash script to include the specific Java test file in the JUnit test command. So, without specifying the test file, JUnit wouldn't be able to identify which file to use. Now, it successfully detects and runs all the test cases.


Student:Also I encountered a problem where one of my test cases (test1) did not pass, and I'm uncertain about the reason for its failure. The method in question was designed to reverse the elements of the input list. Yet, it appears that the list remained unchanged after the method was applied.
Here is my screen shoot of fail test and my code.

![image](https://raw.githubusercontent.com/zmc0806/cse15l-lab-report5/main/mycode.jpeg)

TA: You can try by yourself according print the result before using this method and after using this method.

Student: Thanks!The issue is my test code lies in the assertion part of the test case. In my test,I am comparing the `output` array with the `input` array using `assertArrayEquals`, but I should be comparing the `output` array with the result returned by the `reversed` method. Here's the corrected test case:

```java
import static org.junit.Assert.*;
import org.junit.*;

public class ArrayTests {

  @Test
  public void test1(){
    int[] input = {1, 2, 3, 4, 5, 6};
    int[] expectedOutput = {6, 5, 4, 3, 2, 1};
    int[] actualOutput = ArrayExamples.reversed(input);
    assertArrayEquals(expectedOutput, actualOutput);
  }

}
```

In this corrected version:

- `expectedOutput` is what you expect after the array is reversed.
- `actualOutput` is the result of calling `ArrayExamples.reversed(input)`.
- The `assertArrayEquals` method is used to check if these two arrays are equal.
- 
![image](https://raw.githubusercontent.com/zmc0806/cse15l-lab-report5/main/newtest.jpeg)

Summary:

The file and directory:

The directory is lab3 and in this directory it has these files:
test.sh, ListExamples.java, ArrayTests.java

lib directory - (hamcrest-core-1.3.jar and junit-4.13.2.jar)

These file before fixing the bug:

test.sh (JUnit test command):

```
set -e

javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java
java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore

```

ArrayTests.java (the bug before fixing):

```
import static org.junit.Assert.*;
import org.junit.*;

public class ArrayTests {
  @Test
  public void test1(){
    int[] input = {1,2,3,4,5,6};
    int[] output = {6,5,4,3,2,1};
    System.out.println(ArrayExamples.reversed(input));
    assertArrayEquals(output, input);
  }

}

```

ListExamples.java:

```
public class ArrayExamples {

  // Changes the input array to be in reversed order
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }

  // Returns a *new* array with all the elements of the input array in reversed
  // order
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
        newArray[arr.length - i - 1] = arr[i];
    }
    return newArray;
}


  // Averages the numbers in the array (takes the mean), but leaves out the
  // lowest number when calculating. Returns 0 if there are no elements or just
  // 1 element in the array
  static double averageWithoutLowest(double[] arr) {
    if(arr.length < 2) { return 0.0; }
    double lowest = arr[0];
    for(double num: arr) {
      if(num < lowest) { lowest = num; }
    }
    double sum = 0;
    for(double num: arr) {
      if(num != lowest) { sum += num; }
    }
    return sum / (arr.length - 1);
  }


}

```



Both bugs is caused by when run bash test.sh.

what to edit to fix the bug:

For first bug:To address the initial issue in the bash script, I modified the command to position the target Java file (ArrayTests) at the end of the java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore command line. This adjustment ensures that JUnit correctly identifies the Java file to be tested.

For second bug:For resolving the second bug, create a new variable.This change is intended to capture the altered array returned by the method, thereby updating the array's content to align with the expected results.In my test,I am comparing the `output` array with the `input` array using `assertArrayEquals`, but I should be comparing the `output` array with the result returned by the `reversed` method.

## Part 2 – Reflection

In the latter part of this quarter's lab experience, I acquired a deeper understanding and practical skills in Vim and Bash commands, which significantly broadened my technical expertise.

With Vim, an advanced text editor, I learned far more than basic text editing. I explored its unique modal interface, which includes normal, insert, and visual modes, each serving different functions. I became proficient in using powerful Vim commands for efficient text manipulation, such as 'dd' for deleting a line and 'yy' for copying a line. I also discovered the use of Vim macros, which allow recording and replaying sequences of commands, greatly enhancing my productivity in editing complex files.

In addition, I delved into customizing the Vim environment through the .vimrc configuration file, tailoring the editor to my preferences and workflow. This included setting up custom key bindings, changing color schemes, and installing plugins like 'NERDTree' for directory exploration and 'Syntastic' for syntax checking.

On the Bash side, I deepened my understanding of command-line operations in Unix/Linux environments. I learned to write more sophisticated Bash scripts, incorporating loops, conditionals, and functions to automate routine tasks. I explored various text processing tools like grep, sed, and awk, which are incredibly useful for searching and manipulating data within files.

Furthermore, I gained skills in file system navigation and manipulation, understanding commands like 'cd', 'ls', 'mkdir', and 'rm', and learned to use pipes and redirection to combine commands and manage input/output effectively. I also explored process management with commands like 'top' and 'ps', and job control with 'fg', 'bg', and 'jobs', which are essential for multitasking in a command-line environment.

This newfound knowledge in Vim and Bash has not only made me more adept in handling lab assignments but also equipped me with tools and techniques that are broadly applicable in software development, data analysis, and system administration. The efficiency and versatility that these skills provide have been a game changer in my approach to technical challenges.


