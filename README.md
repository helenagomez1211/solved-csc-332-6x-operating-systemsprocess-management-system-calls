Download Link: https://assignmentchef.com/product/solved-csc-332-6x-operating-systemsprocess-management-system-calls
<br>



This handout describes the <strong>exec </strong>family of functions, for executing a comand. You can use these functions to make a child process execute a new program after it has been forked. The functions in this family differ in how you specify the arguments, but otherwise they all do the same thing. They are declared in the header file ’unistd.h’.

<strong>execv (char *filename, char *const argv[])</strong>

The execv function executes the file named by filename as a new process image.

The argv argument is an array of null-terminated strings that is used to provide a value for the argv argument to the main function of the program to be executed. The last element of this array <em>must </em>be a null pointer.

<strong>execvp (char *filename, char *const argv[])</strong>

The execvp function is similar to execv, except that it searches the directories listed in the PATH environment variable to find the full file name of a file from filename if filename does not contain a slash.

This function is useful for executing system utility programs, because it looks for them in the places that the user has chosen. <strong>Shells use </strong>execvp <strong>to run the commands </strong>that users type.

<strong>execl (char *filename, const char *arg0, …)</strong>

This is similar to execv, but the argv strings are specified individually instead of as an array. A null pointer must be passed as the last such argument.

<strong>execlp (char *filename, const char *arg0, …)</strong>

This function is like execl, except that it performs the same file name searching as the execvp function.

<strong>Example 1: </strong>Using execv(…) command

Note: This version will not search the path, so the full name of the executable file must be given. Parameters to main() are passed in a single array of character pointers.

#include &lt;stdio.h&gt; #include &lt;unistd.h&gt;

int main (int argc, char *argv[])

{ execv (“/bin/echo”, &amp;argv[0]); printf (“EXECV Failed
”);

/* The above line will be printed only on error and not otherwise */

}

Sample Output

$ gcc execv_ex1.c -o execv_ex1 $ ./execv_ex1 Hello World! Hello World!

<strong>Example 2: </strong>Using execvp(…) command

Note: This version searches the path, so the full name of the executable need not be given. Parameters to main() are passed in a single array of character pointers. <em>This is the form used inside a shell!</em>

#include &lt;stdio.h&gt; #include &lt;unistd.h&gt;

int main (int argc, char *argv[])

{ execvp (“echo”, &amp;argv[0]); printf (“EXECVP Failed
”);

/* The above line will be printed only on error and not otherwise */

}

Sample Output

$ gcc execvp_ex2.c -o execvp_ex2 $ ./execvp_ex2 Hello World! Hello World!

<strong>Instructions</strong>

<ul>

 <li>Read man page of exec system call: man exec, to know the syntax of all the four variants in detail</li>

 <li>Compile and execute the examples 1 and 2 to get a feel on how these system call works before you start working on task 3.</li>

 <li>You may also be interested to look at the following link to gain understanding of the process control concepts. <a href="http://www.cs.uregina.ca/Links/class-info/330/Fork/fork.html">http://www.cs.uregina.ca/Links/class-info/330/Fork/fork.html</a></li>

</ul>

<strong>TASK 3</strong>

<strong>Part 1 </strong>Write a program where a child is created to execute command that tells you the date and time in Unix.

Use execl(…).

Note, you need to specify the full path of the file name that gives you date and time information.

Announce the successful forking of child process by displaying its PID.

<strong>Part 2 </strong>Write a program where a child is created to execute a command that shows all files (including hidden files) in a directory with information such as permissions, owner, size, and when last modified. Use execvp(…).

For the command to list directory contents with various options, refer the handout on Unix file system sent to you in the first class.

Announce the successful forking of child process by displaying its PID.

<strong>Part 3</strong>

<strong>[Step 1] Prcs_P1.c: </strong>Create two files namely, destination1.txt and destination2.txt with read, write, and execute permissions.

<strong>[Step 2] Prcs_P2.c: </strong>Copy the contents of source.txt<a href="#_ftn1" name="_ftnref1"><sup>[1]</sup></a> into destination1.txt and destination2.txt as per the following procedure.

<ol>

 <li>Read the next 100 characters from source.txt, and among characters read, replace each character ’1’ with character ’A’ and all characters are then written in destination1.txt</li>

 <li>Then the next 50 characters are read from source.txt, and among characters read, replace each character ’2’ with character ’B’ and all characters are then written in destination2.txt.</li>

 <li>The previous steps are repeated until the end of file source.txt. The last read may not have 100 or 50 characters.</li>

</ol>

Once you’re done with successful creation of executables for the above two steps do the following.

Write a C program and call it Parent_Prcs.c. Execute the files as per the following procedure using execv system call. Use sleep system calls to introduce delays.

<strong>[Step 3] </strong>Fork a child process, say Child 1 and execute Prcs_P1. This will create two destination files according to Step 1.

<strong>[Step 4] </strong>After Child 1 finishes its execution, fork another child process, say Child 2 and execute Prcs_P2 that accomplishes the procedure described in Step 2.


