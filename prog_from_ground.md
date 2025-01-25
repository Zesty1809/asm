# Programming from the ground up <!-- omit in toc -->

- [Chapter 1 Introduction](#chapter-1-introduction)

## Chapter 1 Introduction

Linux is the name of the kernel. The kernel is the core part of an operating system that keeps track of everything. The kernel is both an fence and a gate. As a gate, it allows programs to access hardware in a uniform way. Without the kernel, you would have to write programs to deal with every device model ever made. The kernel handles all device-specific interactions so you don't have to. It also handles file access and interaction between processes. For example, when you type, your typing goes through several programs before it hits your editor. First, the kernel is what handles your hardware, so it is the first to receive notice about the keypress. The keyborad sends in scancodes to the kernel, which then converts them to the actual letters, numbers, and symbols they represent. If you are using a windowing system, then the windowing system reads the keypress from the kernel, and delivers it to whatever program is currently in focus on the user's display.

Example 1-1. How the computer processes keyboard signals
Keyboard -> Kernel -> Windowing system -> Application program

As a fence, the kernel prevents programs from accidentally overwriting each other's data and from accessing files and devices that they don't have permission to. It limits the amount of damage a poorly-written program can do to other running programs.

There are essentially three kinds of languages:

Machine Language
