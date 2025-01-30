# Introduction

The most basic program in C language is to print Hello World! into the console. The following code shows how we can do it:
1. Create a file `hello.c` and copy this code into the file and save it.

```c
#include <stdio.h>

int main(void)
{
  printf("Hello World!\n");
  return 0;
}
```

2. Then run the following commands in the terminal to compile it and run it.


```bash
$ gcc hello.c -o hello
$ ./hello
```

3. The following output is displayed in the terminal.

```bash
$ Hello World!
```

## Understanding Your First Program

The first line of the program

```c
#include <stdio.h>
```

tells the compiler to include the header file `stdio.h` in our source code. Header files are files with `.h` extension. `#include` is a preprocessor directive which tells the compiler to include the file following with the name follwing the command. `stdio.h` is the header file known as standard input and output. It contains function prototypes of functions such as `printf`, `scanf`. 

In simpler words, the compiler does not know how the printf function works. So to make it understand we need to include the standard input and output header file.

The next line

```c
int main(void)
```

marks the beginning of a program. The `int` keyword defines that the current function returns an integer. `main()` defines the name of the function. Every program should have a main function as it is the point from where execution begins. Without the main function the computer would have no idea from where to begin the execution of a program. 

The parenthesis after the name of the function contains the function parameters or in simple terms input of the function. The `void` keyword inside the parenthesis informs the system that the `main` function takes no argument.

The opening and closing closing braces contains the body of the program. All the statements of a function should be contained within these braces. In this case, all the statements of the main function should be enclosed within the curly braces.

The line

```c
printf("Hello World!\n");
```
tells the computer to display the string within the double quotation marks ("") in the terminal. The `printf()` function displays the argument that it is provided with. All statements in C must be terminated with a semicolon. The backslash n `\n` keyword adds a newline character after the output.

The last statement

```c
return 0;
```

return to the system a status value of 0. You can use any integer here. Zero is used by convention to indicate that the program completed successfully. Different numbers can be used to indicate different types of errors.
