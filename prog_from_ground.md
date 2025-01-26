# Programming from the ground up <!-- omit in toc -->

- [Chapter 1. Introduction](#chapter-1-introduction)
  - [Machine Language](#machine-language)
  - [Assembly Language](#assembly-language)
  - [High-Level Language](#high-level-language)
- [Chapter 2. Computer Architecture](#chapter-2-computer-architecture)
  - [Memory](#memory)
  - [The CPU](#the-cpu)
  - [Some Terms](#some-terms)
  - [Data Accessing Methods](#data-accessing-methods)
- [Chapter 3. Your First Programs](#chapter-3-your-first-programs)
  - [Entering in the Program](#entering-in-the-program)
  - [Outline of An Assembly Language Program](#outline-of-an-assembly-language-program)
  - [Planning the Program](#planning-the-program)
  - [Finding a Maximum Value](#finding-a-maximum-value)

## Chapter 1. Introduction

&nbsp;&nbsp;Linux is the name of the kernel. The kernel is the core part of an operating system that keeps track of everything. The kernel is both an fence and a gate. As a gate, it allows programs to access hardware in a uniform way.

&nbsp;&nbsp;Without the kernel, you would have to write programs to deal with every device model ever made. The kernel handles all device-specific interactions so you don't have to. It also handles file access and interaction between processes. For example, when you type, your typing goes through several programs before it hits your editor.

&nbsp;&nbsp;First, the kernel is what handles your hardware, so it is the first to receive notice about the keypress. The keyborad sends in scancodes to the kernel, which then converts them to the actual letters, numbers, and symbols they represent. If you are using a windowing system, then the windowing system reads the keypress from the kernel, and delivers it to whatever program is currently in focus on the user's display.

Example 1-1. How the computer processes keyboard signals
Keyboard -> Kernel -> Windowing system -> Application program

As a fence, the kernel prevents programs from accidentally overwriting each other's data and from accessing files and devices that they don't have permission to. It limits the amount of damage a poorly-written program can do to other running programs.

There are essentially three kinds of languages:

### Machine Language

&nbsp;&nbsp;This is what the computer actually sees and deals with. Every command the computer sees is given as a number or sequence of numbers.

### Assembly Language

&nbsp;&nbsp;This is the same as machine language, except the command numbers have been replaced by letter sequences which are easier to memorize. Other small things are done to make it easier as well.

### High-Level Language

&nbsp;&nbsp;High-Level Languages are there to make programming easier. Assembly language requires you to work with the machine itself. High-level languages allow you to describe the program in a more natural language. A single command in a high-level language usually is equivalent to several commands in an assembly language.

## Chapter 2. Computer Architecture

### Memory

The computer's memory is used for a number of different things. All the results of any calculations are stored in memory. In fact, everything that is "stored" is stored in the memory.

The Von Neumann architecture specifies that not only computer data should live in memory, but the programs that control the computer's operation should live there, too. In face, in a computer, there is no difference between a program and a program's data except how it is used by the computer. They are both stored and accessed the same way.

### The CPU

The CPU reads in instructions from memory one at a time and executes them. This is known as the *fetch-execute cycle*. The CPU contains the following elements to accomplish this:

- Program Counter
- Instruction Decoder
- Data bus
- General-purpose registers
- Arithmetic and logic unit

The *program counter* is used to tell the computer where to fetch the next instruction from. We mentioned earlier that there is no difference between the way data and programs are stored, they are just interpreted differently by the CPU. The program counter holds the memory address of the next instruction to be executed. The CPU begins by looking at the program counter, and fetching whatever number is stored in memory at athe location specified. It is then passed on to the *instruction decoder* which figures out what the instruction means. This includes what process needs to take place (addition, subtraction, multiplication, data movement, etc.) and what memory locations are goins to be involved in this process. Computer instructions usually consist of both the actual instruction and the list of memory locations that are used to carry it on.

Now the computer uses the *data bus* to fetch the memory locations to be used in the calculation. The data bus is the connection between the CPU and memory. It is the actual wire that connects them. If you look at the motherboard of the computer, the wires that go out from the memory are your data bus.

In addition to the memory on the outside of the processor, the processor itself has some special, high-speed memory locations called registers. There are two kinds of registers - *general purpose registers* and *special-purpose registers*. General-purpose registers. General-purpose registers are where the main action happens. Addition, subtraction, multiplication, comparisions, and other operations generally use general-purpose registers for processing. However, computers have very few general-purpose registers. Most information is stored in main memory, brought in to the registers for processing, and then put back into memory when the processing is completed. Special-purpose registers are registers which have very specific purposes. We will discuss these as we come to them.

Now that the CPU has retrieved all of the data it needs, it passes on the data and the decoded instruction to the *arithmetic and logic unit* for further processing. Here the instruction is actually executed. After the results of the computations have been calculated, the results are then placed on the data bus and sent to the appropriate location in memeory or in a register, as specified by the instruction.

This is very simplified explanation. Processors have advanced quite a bit in recent years, and are now much more complex. Although the basic operation is still the same, it is complicated by the use of cache hierarchies, superscalar processors, pipelining, branch prediction, out-of-order execution, microcode translation coprocessors, and other optimizations. 

### Some Terms

Computer memory is a numbered sequence of fixed-size storage locations. The number attached to each storage location is called it's *address*. The size of a single storage location is called a byte. On x86 processors, a byte is a number between 0 and 255.

You may be wondering how computers can display and use text, graphics, and even large numbers when all they can do is store numbers between 0 and 255. First of all, specialized hardware like graphics cards have special interpretations of each number. When displaying to the screen, the computer uses ASCII code tables to translate the numbers you are sending it into letters to display on the screen, with each number translating to exactly one letter or numberal. For example, the capital letter A is represented by the number 65. The numberal 1 is represented by the number 49. So, to print out "HELLO", you would actually give the computer the sequence of numbers 72, 69, 76, 76, 79. To print out the number 100, you would give the computer the sequence of numbers 49, 48, 48. A list of ASCII characters and their numeric codes is found in this link{**todo**}.

In addition to using numbers to represent ASCII characters, you as the programmer get to make the numbers mean any thing you want them to, as well. For example, if I am running a store, I would use a number to represent each item I was selling. Each number would be linked to a series of other numbers which would be ASCII codes for what I wanted to display when the items were scanned in. I would have more numbers for the price, how many I have in inventory, and so on.

We mentioned earlier that in addition to the regular memory that the computer has, it also has special-purpose storage locations called *registers*. Registers are what the computer uses for computation. Registers keep the contents of numbers that you are currently manipulating.

On the computers we are using, registers are each four bytes long. The size of a typical register is called a computer's *word* size. x86 processors have four-byte words. This means that it is most natural on these computers to do computations four bytes at a time. This gives roughly 4 billion values.

Addresses are also four bytes (1 word) long, and therefore also fit into a register. x86 processors can access up to 4294967296 bytes if enough memory is installed. Notice that this means that we can store addresses the same way we store any other number. In fact, the computer can't tell the difference between a value that is an address, a value that is a number, a value that is an ASCII code, or a value that you have decided to use for another purpose. A number becomes an ASCII code when you attempt to display it. A number becomes an address when you try to look up the byte it pointss to.

Addresses which are stored in memory are also called *pointers*, because instead of having a regular value in them, they point you to a different location in memory.

As we've mentioned, computer instructions are also stored in memory. In fact, they are stored exactly the same way that other data is stored. The only way the computer knows that a memory location is an instruction is that a special-purpose register called the instruction pointer points to them at one point or another. If the instruction pointer pooints to a memory word, it is loaded as an instruction. Other than that, the computer has no way of knowing the difference between programs and other types of data.

### Data Accessing Methods

Processors have a number of different ways of accessing data, known as addressing modes. The simplest mode is *immediate mode*, in which the data to access is embedded in the instruction itself. For example, if we want to initialize a register to 0, instead of giving the computer an address to read the 0 from, we would specify immediate mode, and give it the number 0.

In the *register addressing mode*, the instruction contains a register to access, rather than a memory location. The rest of the modes will deal with addresses.

In the *direct addressing modes*, the instruction contains the memory address to access. For example, I could say, please load this register with the data at address 2002. The computer would go directly to byte number 2002 and copy the contents into out register.

In the *indexed addressing mode*, the instruction contains a memory address to access, and also specifies an *index register* to offset that address. For example, we could specify address 2002 and an index register. If the index register contains the number 4, the actual address the data is loaded from would be 2006. This way, if you have a set of numbers starting at location 2002, you can cycle between each of them using index register. On x86 processors, you can also specify a *multiplier* for the index. This allows you to access memory a byte at a time or a word at a time (4 bytes). If you are accessing an entire word, your index will need to be multiplied by 4 to get the exact location of the fourth element from your address. For example, if you wanted to access the fourth byte from location 2002, you woulld load your index register with 3 (remember, we start counting at 0) and set the multiplier to 1 since you are going a byte at a time. This would get you location 2005. However, if you wanted to access the fourth word from location 2002, you would load your index register with 3 and set the multiplier to 4. This would load from location 2014 - the fourth word.

In the *indirect addressing mode*, the instruction contains a register that contains a pointer to where the data should be accessed. For example, if we used indirect addressing mode and specified the %eax register, and the %eax register contained the value 4, whatever value was at memory location 4 would be used. In direct addressing, we would just load the value 4, but in indirect addressing, we use 4 as the address to use to find the data we want.

Finally, there is the *base pointer addressing mode*. This is similar to indirect addressing, but you also include a number called the *offset* to add to the register's value before using it for lookup. 

## Chapter 3. Your First Programs

### Entering in the Program

Okay, this first program is simple. In fact, it's not going to do anything but exit! It's short, but it shows some basics about assembly language and Linux programming. You need to enter the program in an editor exactly as written, with the filename *exit.s*. The program follows. Don't worry about not understanding it. This section only deals with typingg it in and running it. In the Section called *Outline of an Assembly Language Program* we will describe how it works.

```nasm
# PURPOSE: Simple program that exits and returns a
#          status code back to the linux kernel
#

# INPUT: none
#

# OUTPUT: returns a status code. This can be viewed
#         by typing
#
#         echo $?
#
#         after running the program
#

# VARIABLES: 
#         %eax holds the system call number
#         %ebx holds the return status
#

.section .data

.section .text
.globl _start
_start:
  /* This is a linux kernel command
  number (system call) for exiting
  a program */ 
  movl $1, %eax   

  /* This is the status number we will
  return to the operating system.
  Change this around and it will
  return different things to
  echo $? */
  movl $0, %ebx

  /* this wakes up the kernel to run
  the exit command */
  int $0x80

```

Whay you typed in is called the *source code*. Source code is the human-readable form of program. In order to transform it inot a program that a computer can run, we need to *assemble* and *link* it.

The first step is to assemble it. Assembling is the process that transforms what you typed into instructions for the machine. The machine itself only reads sets of numbers, but humans prefer words. An *assembly language* is a more human-readable form of the instructions a computer understands. Assembling transforms the human-readable file into a machine-readable one. To assemble the program type in the command

```bash
as exit.s -o exit.o
```

*as* is the command which runds the assembler, *exit.s* is the source file, and *-o exit.o* tells the assembler to put it's output in the file *exit.o*. *exit.o* is an *object file*. An object file is code that is in machine's language, but has not been completely put together. In most large programs, you will have several source files, and you will comvert each one into an object file. The *linker* is the program that is responsible for putting object files together and adding information to it so that the kernel know how to load and run it. In our case, we only have one object file, sot the linker is only adding the information to enable it to run. To *link* the file, enter the command

```bash
ld exit.o -o exit
```

*ld* is the command to run the linker, *exit.o* is the object file we want to link, and *-o exit* instructs the linker to output the new program into a file called *exit*. If any of these commands reported errors, you have either mistyped your program or the command. After correcting the program, you have to re-run all the commands. *You must always re-assemble and re-link programs after you modify the source file for the changes to occur in the program.* You can run *exit* by typing in the command

```bash
./exit
```

The *./* is used to tell the computer that the program isn't in one of the normal program directories, but is in the current directory instead. You'll notice when you type this command, the only thing happens is that you'll go to the next line. That's because this program does nothing but exit. However, immediately after you run the program, if you type in

```bash
echo $?
```

It will say *0*. What is happening is that every program when it exits gives Linux an exit status code, which tells it if everything went all right. If everything was okay, it returns 0. UNIX programs return numbers other than zero to indicate failure or other errors, warnings, or statuses. The programmer determines what each number means. You can view this code by typing in *echo $?*.

### Outline of An Assembly Language Program

Take a look at the program we just entered. At the beginning there are lots of lines that begin with hashes (#). These are *comments*. Comments are not translated by the assembler. They are used only for the programmer to talk to anyone who looks at the code in the future. Most programs you write will be modified by other. Get into habit of writing comments in your code that will help them understand both why the program exists and how it works. Always include the following in your comments:

- The purpose of the code
- An overview of the processing involved
- Anything strange your program does and why it does it

After the comments, the next line says

```nasm
.section .data
```

Anything starting with a period isn't directly translated into a machine instruction. Instead, it's an instruction to the assembler itself. These are called *assembler directives* or *pseudo-operations* because they are handled by the assembler and are not actually run by the computer. The *.section* command breaks your program into sections. This command starts the data section, where you list any memeory storage you will need for data. Our program doesn't use any, so we don't need the section. It's just here for completeness. Almost every program you write in the future will have data.

Right after this you have

```nasm
.section .text
```

which starts the text section. The text section of a program is where the program instructions live.

The next instruction is

```nasm
.globl _start
```

This instructs the assembler that _start is important to remember. *_start* is a *symbol*, which means that it is going to be replaced by something else either during assembly or linking. Symbols are generally used to mark locations of programs or data, so you can fefer to them by name insted of by their location number. Imagine if you had to refer to every memeory location by it's address. First of all, it would be very confusing because you would have to memorize or look up the numeric memory address of every piece of code or data. In addition, every time you had to insert a piece of data or code you would have to change all the addresses in your program! Symbols are used so that the assembler and linker can take care of keeping track of addresses, and you can concentrate on writing your program. *.globl* means that the assembler shouldn't discard this symbol after assembly, because the linker will need it. *_start* is special symbol that always needs to be marked with *.globl* because it marks the location of the start of the program. *Without marking this location in this way, when the computer loads your program it won't know where to begin running your program.*

The next line 

```nasm
_start:
```

*defines* the value of the *_start* label. A *label* is a symbol followed by a colon. Labels define a symbol's value. When the assembler is assembling the program, it has to assign each data value and instruction an address. Labels tell the assembler to make the symbol's value be wherever the next instruction or data element will be. This way, if the actual physical location of data or instruction changes, you don't have to rewrite any refrences to it - the symbol automatically gets the new value.

Now we get into actual computer instructions. The first such instruction is this:

```nasm
movl $1, %eax
```

When the program runs, this instruction transfers the number 1 into the %eax register. In assembly language, many instructions have *operands*. *movl* has two operands - the *source* and the *destination*. In this case, the source is the literal number 1, and the destination is the *%eax* register. Operands can be numbers, memory location references, or registers. Differentj instructions allow different types of operands. Different instructions allow different types of operands.

On most instructions which have two operands, the first one is the source operand and the second one is the destination. Note that in these cases, the source operand is not modified at all. Other instructions of this type are, for example, *addl*, *subl*, and *imull*. These add/subtract/multiply the source operand from/to/by the destination operand and save the result in the destination operand. Other instructions may have an operand hardcoded in. *idivl*, for example, requires that the dividend be in *%eax*, and *%edx* be zero, and the quotient is then transferred to *%eax* and the remainder to *%edx*. However, the divisor can be any register or memory location.

On x86 processors, there are several general-purpose registers (all of which can be used with movl):

- %eax
- %ebx
- %ecx
- %edx
- %edi
- %esi

In addition to those general-purpose registers, there are also several special-purpose registers, including:

- %ebp
- %esp
- %eip
- %eflags

We'll discuss these later, just be aware that they exist. Some of these registers, like %eip and %eflags can only be accessed through special instructions. The others can be accessed using the same instruction as general-purpose registers, but they have special meanings, special uses, or are simply faster when used in a specific way.

So, the *movl* instruction moves the number 1 into %eax. The dollar-sign in front of the one indicates that we want to use immediate mode addressing (refer back to the Section called Data Accessing Methods in Chapter 2). Without the dollar-sign it would do direct addressing, loading whatever number is at address 1. We want the actual number *1* loaded in, so we have to use immediate mode.

The reason we are moving the number 1 into *%eax* is because we are preparing to call the Linux Kernel. The number 1 is the number of the *exit system call*. We will discuss system calls in more depth soon, but basically they are requests for the operating system's help. Normal programs can't do everything. Many operations such as calling other programs, dealing with files, and exiting have to be handled by the operating system through system calls. when you make a *system call*, which we will do shortly, the system call number has to be loaded into %eax. Depending on the system call, other registers may have to have values in them as well. Note that system calls is not the only use or even the main use of registers. It is just the one we are dealing with in this first program. Later programs will use registers for regular computation.

The operating system, however, usually needs more information than just which call to make. For example, when dealing with files, the operating system needs to know which file you are dealing with, what data you want to write, and other details. The extra details, called *parameters* are stored in other registers. In the case of the *exit* system call, the operating system requires a status code be loaded in *%ebx*. This value is then returned to the system. This is the value you retrieved when you typed *echo $?*. So, we load *%ebx* with *0* by typing the following:

```nasm
movl $0, %ebx
```

Now, loading registers with these numbers doesn't do anything itself. Registers are used for all sorts of things besides system calls. They are where all program logic such as addition, subtraction, and comparisons take place. Linux simply requires that certain registers be loaded with certain parameter values before making a system call. *%eax* is always required to be loaded with the system call number. For the other registers, however, each system call has different requirements. In the *exit* system call, *%ebx* is required to be loaded with the exit status. 

The next instruction is the "magic" one. It looks like this:

```nasm
int $0x80
```

The *int* stands for *interrupt*. The *0x80* is the interrupt number to use. An *interrupt* interrupts the normal program flow, and transfers control from our program to Linux so that it will do a system call.

### Planning the Program

In our next program we will try to find the maximum of a list of numbers. Computers are very detail-oriented, so in order to write the program we will have to have planned out a number of details. These details include:

- Where will the original list of numbers be stored?
- What procedure will we need to follow to find the maximum number?
- How much storage do we need to carry out that procedure?
- Will all of the storage fit into registers, or do we need to use some memory as well?

In computers, you have to plan every step of the way. So, let's do a little planning. First of all, just for reference, let's name the address where the list of numbers starts as *data_items*. Let's say that the last number in the list will be a zero, so we know where to stop. We also need a value to hold the current position in the list, a value to hold the current list element being examined, and the current highest value on the list. Let's assign each of these a register:

- %edi will hold the current position in the list.
- %ebx will hold the current highest value in the list.
- %eax will hold the current element being examined.

When we begin the program and look at the first item in the list, since we haven't seen any other items, that item will automatically be the current largest element in the list. Also, we will set the current position in the list to be zero - the first element. From then, we will follow the following steps:

1. Check the current list element (%eax) to see if it's zero (the terminating element).
2. If it is zero, exit.
3. Increase the current position (%edi).
4. Load the next value in the list into the current value register (%eax). What addressing mode might we use here? Why?
5. Compare the current value (%eax) with the current highest value (%ebx).
6. If the current value is greater than the current highest value, replace the current highest value with the current value.
7. Repeat

That is the procedure. many times in that procedure I made use of the word "if". These places are where decisions are to be made.

These "if"'s are a class of instructions called *flow control* instructions, because they tell the computer which steps to follow and which paths to take. This program is much more dynamic and is directed by data. Depending on what data it receives, it will follow different instruction paths.

In this program, this will be accomplished by two different instructions, the conditional jump and the unconditional jump. The conditional jump changes path based on the results of a previous comparison or calculation. The unconditional jump just goes directly to a different path no matter what. The unconditional jump may seem useless, but it is very necessary since all of the instructions will be laid out on a line. If a path needs to converge back to the main path, it will have to do this by an unconditional jump. 

Another use of flow control is in implementing loops. A loop is a piece of program code that is meant to be repeated. In our example, the first part of the program (setting the current position to 0 and loading the current highest value with the current value) was only done once, so it wasn't a loop. However, the next part is repeated over and over again for every number in the list. It is only left when we have come to the last element, indicated by zero. This is called a *loop* because it occurs over and over again. It is implemented by doing unconditional jumps to the beginning of the loop at the end of the loop, which causes it to start over. However, you have to always remember to have a conditional jump to exit the loop somewhere, or the loop will continue forever! This condition is called an *infinite loop*. If we accidently left out step 1, 2, or 3, the loop (and our program) would never end.

In the next section, we will implement this program that we planned.

### Finding a Maximum Value

Enter the following program as *maximum.s*:

```nasm
.section .data
data_items:
  .long 3, 67, 35, 222, 47, 76, 85, 44, 33, 22, 11, 99, 0

.section .text

.globl _start
_start:
  movl $0, %edi
  movl data_items(,%edi,4), %eax
  movl %eax, %ebx

start_loop:
  cmpl $0, %eax
  je loop_exit
  incl %edi
  movl data_items(,%edi,4), %eax
  cmpl %ebx, %eax
  jle start_loop

  movl %eax, %ebx

  jmp start_loop

loop_exit:
  movl $1, %eax
  int $0x80

```
