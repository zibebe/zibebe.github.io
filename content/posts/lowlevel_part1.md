+++
title = "Low Level Programming: Part 1"
date = "2024-12-08"

[taxonomies]
tags=["programming","c"]
+++

In this course, I will guide you through the essentials of low-level
programming, starting with the fundamentals of C programming. This foundation
will be crucial for understanding the more advanced topics that follow. While
some basic programming knowledge is helpful, this course is designed to be
accessible to those with a beginner to intermediate skill level.

## Setup

### Compiler

To get started with this course, you need to set up the necessary tools. The
first step is to ensure you have a C compiler installed, such as `gcc`. You can
refer to the [official installation manual](https://gcc.gnu.org/install/) for
detailed instructions, or you can use your operating system's package manager to
install it. Here are some quick commands for popular operating systems:

- **Installation (Linux/macOS):**

  ```sh
  sudo apt-get install gcc  # Debian/Ubuntu
  sudo dnf install gcc      # Fedora
  brew install gcc          # macOS
  ```

- **Installation (Windows):** You can install MinGW, which includes `gcc`.
  Follow the instructions on the
  [MinGW website](https://mingw-w64.org/doku.php/download).

### Text Editor

While the choice of editor or integrated development environment (IDE) is
largely a matter of personal preference, I recommend using a terminal-based
editor for this course. This is because we will be working extensively in the
terminal. I absolutely recommend getting started with `Vim` as a terminal
editor:

- **Installation (Linux/macOS)**

  ```sh
  sudo apt-get install vim  # Debian/Ubuntu
  sudo dnf install vim      # Fedora
  brew install vim          # macOS
  ```

- **Installation (Windows):** Follow the instructions on the
  [Vim website](https://www.vim.org/download.php).

Anyhow, choose the tool that you are most comfortable with, and you'll be
well-prepared to follow along with the course.

### Test the Setup

To ensure your environment is set up correctly, we will create a simple "Hello
World" program. Follow these steps:

1. **Create the `hello_world.c` file:**

   Open your chosen editor or IDE and create a new file named `hello_world.c`.
   Add the following content to the file:

   ```c
   #include <stdio.h>

   int main(int argc, char **argv) {
       printf("Hello World!\n");
       return 0;
   }
   ```

2. **Compile the Program:**

   Open a terminal and navigate to the directory where you saved
   `hello_world.c`. Compile the program using the following command:

   ```sh
   gcc hello_world.c -o hello_world
   ```

3. **Run the Program:**

   Execute the compiled binary by running:

   ```sh
   $ ./hello_world
   Hello World!
   ```

   If you encounter any issues, double-check that your compiler and editor are
   installed correctly and that you are in the correct directory when running
   the commands.

## Memory Management

Understanding memory management is crucial for effective low-level programming,
as it directly impacts the performance, reliability, and efficiency of your
code. Here is a short comparison between `Static`, `Stack`, and `Heap`:

### Static

- **Lifetime**: Variables are allocated at compile time and exist for the entire
  duration of the program. They are not created or destroyed during runtime.
- **Size**: The size is fixed and determined at compile time.

- **Speed**: Accessing static variables is relatively fast because they have a
  fixed memory location.
- **Usage**: Ideal for global variables, static local variables, and constants
  that need to retain their value across function calls and throughout the
  program's execution.

### Stack

- **Lifetime:** Variables are allocated on the stack with a known, fixed
  lifetime (usually tied to function scope).
- **Size:** The memory is managed automatically; variables go out of scope when
  their containing block ends.
- **Speed:** Accessing variables stored in the stack is faster because they have
  contiguous memory and direct access.
- **Usage:** Ideal for local variables and function call parameters. Each
  function has its own stack frame.

### Heap

- **Lifetime:** Memory allocated on the heap can persist beyond the lifetime of
  a single function (until explicitly deallocated).
- **Size:** The size is flexible; it can grow or shrink dynamically during
  program execution.
- **Speed:** Accessing variables stored in the heap is slower because there's no
  direct access and more indirection through pointers.
- **Usage:** Ideal for dynamic memory allocation, such as when allocating large
  structures that need to persist across function calls.
 summary:

- `Static` provides persistent storage that exists for the entire duration of
  the program.
- `Stack` provides fast but temporary storage, ideal for local variables and
  function parameters.
- `Heap` offers slower but flexible and persistent storage, suitable for dynamic
  memory allocation and large data structures.

If you want to get more informations about memory allocation and management here
are some useful links:

- [Stack-based memory allocation](https://en.wikipedia.org/wiki/Stack-based_memory_allocation)
- [Memory management](https://en.wikipedia.org/wiki/Memory_management)

### Examples in C

1. **Static Variable**

   This little example shows what happens when you declar variables with the
   static keyword.

   ```c
   #include <stdio.h>
   
   static int fglob_x = 42;
   
   void test() {
     static int x = 42;
     x += 7;
     printf("x: %d\n", x);
   }

   int main(void) {
     printf("fglob_x: %d\n", fglob_x);

     for (int i = 0; i < 5; i++) {
       test();
     }

     return 0;
   }
   ```

   The Variable `fglob_x` will be visible for all functions in the file
   above. So, more or less it is a global variable scoped to a specific file.
  
   If you compile and run the program you will see, that the variable `x` in
   the `test` function will keep its value and is not reinitialized with every
   call:
  
     ```sh
     fglob_x: 42
     x: 49
     x: 56
     x: 63
     x: 70
     x: 77
     ```
