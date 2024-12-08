+++
title = "Low Level Programming: Part 1"
date = "2024-12-08"

[taxonomies]
tags=["programming","c"]
+++

In this course i will teach you the essentials about low-level programming. 
Starting with some C programming essentials will give you the foundation for everything that follow.
You will need some basic understanding of programming to follow the course.

# Environment Setup

## Compiler

At first we are going to set up the tools we need to follow the course.
So the first thing is to make sure that you have an C Compiler e.g. `gcc` installed. For this, you could refer to [official installation manual](https://gcc.gnu.org/install/)
or simply use the package manager your OS provides.

## Editor / IDE

As it doesn't really matter which editor you use, you are free to choose any editor. My personal recommendations would be any terminal editor e.g. [vim](https://www.vim.org) or [helix](https://helix-editor.com)
as we live most of the time in this course in a terminal anyway.

## Test the Setup

We test the setup by simply creating a `hello_world.c` file and fill it with the following content.

```c
#include <stdio.h>

int main(int argc, char **argv) {
  printf("Hello World!\n");
  return 0;
}
```

Compile it to a binary with the following command:

```console
$ gcc hello_world.c -o hello_world
```

Run the binary

```console
$ ./hello_world
Hello World!
```

# Memory Allocation

It is very important to understand Memory Allocation before getting started with low level programming.
Here is a short comparison between the `Stack` and `Heap` memory:

## Stack
- **Lifetime:** Variables are allocated on the stack with a known, fixed lifetime (usually tied to function scope).
- **Size:** The memory is managed automatically; variables go out of scope when their containing block ends.
- **Speed:** Accessing variables stored in the stack is faster because they have contiguous memory and direct access.
- **Usage:** Ideal for local variables and function call parameters. Each function has its own stack frame.

## Heap
- **Lifetime:** Memory allocated on the heap can persist beyond the lifetime of a single function (until explicitly deallocated).
- **Size:** The size is flexible; it can grow or shrink dynamically during program execution.
- **Speed:** Accessing variables stored in the heap is slower because there's no direct access and more indirection through pointers.
- **Usage:** Ideal for dynamic memory allocation, such as when allocating large structures that need to persist across function calls.

In summary, the Stack provides ***fast but temporary storage***, while the Heap offers ***slower but persistent storage***.

If you want to get more informations about memory allocation and management here are some useful links:
- [Stack-based memory allocation](https://en.wikipedia.org/wiki/Stack-based_memory_allocation)
- [Memory management](https://en.wikipedia.org/wiki/Memory_management)

# References and Pointers in C
