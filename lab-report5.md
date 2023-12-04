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
