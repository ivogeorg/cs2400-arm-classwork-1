# cs2400-arm-classwork-1

CS2400 ARM assembly programming classwork problems.

## C and assembly code

Follow the instructions for each of the following code samples in [Compliler Explorer](https://godbolt.org).

1. [printf](https://godbolt.org/z/y2YKew)
   1. What is the library function that is called?
   2. Research the implementation (source code) of this function.
   3. Find out if the program directly executes the output operation or it makes a *system call* to the operating system.
   
2. [malloc](https://godbolt.org/z/kAZX7x)
   1. How are the arguments passed to `malloc` and `free`?
   2. Research the implementation (source code) of `malloc` and `free`.
   
3. [malloc array](https://godbolt.org/z/bBl0zx)
   1. How does this case differ from the previous one?
   2. [**hard**] Write your own tiny `malloc` by declaring a large `FILL` area and writing a `malloc` and a `free` subroutine.
   
4. [arrays](https://godbolt.org/z/lcH006)
   1. Port this code to VisUAL.
   2. Observe/show that this code writes the local array in reverse order to the `static` global array.
   
5. [2d array](https://godbolt.org/z/Kr-Sn8)
   1. Port this code to VisUAL.
   2. How are nested `for` loops handled in assembly? Are they *"nested"* in assembly?
   
6. [2d array with mul](https://godbolt.org/z/cHwSTR)
   1. Port this code to VisUAL. (It's the same as the previous but with multiplicatoin).
   2. Add your 32-bit unsigned integer multiplication algorithm as a subroutine and run the code. Verify its correctness.

## Submission
1. Fork this repository
2. Clone and implement.
3. Commit any modifications.
4. Push your commits to your remote.
5. For research-type questions, answer inline in the [README](README.md).

