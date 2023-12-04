## Part 1 – Debugging Scenario

Question 

![image](https://raw.githubusercontent.com/zmc0806/cse15l-lab-report5/main/problem.jpeg)


![image](https://raw.githubusercontent.com/zmc0806/cse15l-lab-report5/main/ed.jpeg)


TA: Alright, I understand your issue. You need to ensure that JUnit is aware of which specific file to test within your bash script.You should adjusting the last line of your bash.

Student: Got it, that makes sense. I've updated the bash script to include the specific Java test file in the JUnit test command. So, without specifying the test file, JUnit wouldn't be able to identify which file to use. Now, it successfully detects and runs all the test cases.


Student:Also I encountered a problem where one of my test cases (test1) did not pass, and I'm uncertain about the reason for its failure. The method in question was designed to reverse the elements of the input list. Yet, it appears that the list remained unchanged after the method was applied.
Here is my screen shoot of fail test and my code.

![image](https://raw.githubusercontent.com/zmc0806/cse15l-lab-report5/main/mycode.jpeg)

