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
.section .data
    # (Data section can be left empty if not used)

.section .text
.globl _start
_start:
    mov $1, %eax        # System call number for exit (sys_exit)
    mov $0, %ebx        # Exit status (0)
    int $0x80           # Trigger system call
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