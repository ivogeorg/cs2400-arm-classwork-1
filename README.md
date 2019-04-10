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
   2. [**hard**] Write your own tiny `malloc` library by declaring a large `FILL` area and writing a `malloc` and a `free` subroutines that manage allocations to that memory area. 
      1. `malloc` works approximately as follows:
         - it takes as argument the number of bytes requested
         - it finds an appropriate region of the heap that can satisfy the request and marks it as allocated
         - it adds a small *metadata* memory block of known size on top of the region and writes the size of the region in the block
         - returns a pointer to the region, not including the metadata block
         - if the allocation fails for any reason (e.g. running out of memory), it returns `NULL` (0x00000000), which is an invalid address for user programs
         - allocates regions in from-lower-to-higher address orientation
      2. `free` works approximately as follows:
         - it takes the pointer returned by `malloc`
         - it subtracts the size of the metadata block from this address
         - it reads the size of the allocated region
         - it marks the cumulative (metadata block + region) previously allocated area as available
      3. Non-interleaving of calls:
         - assume all the calls to `malloc` precede all the calls to `free`
         - assume the `free` calls will be made in the reverse order of the `malloc` calls, as in 
           ```c
           int *p1 = (int *) malloc(200 * sizeof(int));
           int *p2 = (int *) malloc(300 * sizeof(int));
           int *p3 = (int *) malloc(100 * sizeof(int));
           
           // use memory...
           
           free(p3);
           free(p2);
           free(p1);
           ```
         - this relieves you from the responsibility to manage *holes* in the memory area
      4. Variables you will need:
         - `memstore` (standing for _memory store_) - starting address of the fill area
         - `storeptr` (standing for _store pointer_) - a pointer to the next available memory region
      5. Stack:
         - manage the subroutine (aka function) calls by creating stack frames for them to hold their arguments as well as any local variables that are needed
         - don't forget to manage the register bank and not overwrite register value that are needed by the *caller*
         - if you need to save registers on the stack, you can do it within the frame of the *callee*, correctly expanding the frame to fit them (note that VisUAL does not support `push` and `pop`)
         - note that a function's stack frame only lasts between the start and end of execution of the subroutine, regardless of how many times the subroutine is called
   
4. [arrays](https://godbolt.org/z/lcH006)
   1. Port this code to VisUAL.
      - for an example, refer to the [negate repo](https://github.com/ivogeorg/cs2400-arm-asm-negate-exercise.git)
        1. Open the [Compiler Explorer](https://godbolt.org/)
        2. Select the **ARM gcc 8.2** compiler
        3. Enter the following compiler options in the box on the right: `-fomit-frame-pointer -mcpu=cortex-m3 -mtune=cortex-m3`
        4. Put the code of the [`negate.c`](https://github.com/ivogeorg/cs2400-arm-asm-negate-exercise/blob/master/negate.c) file in the left pane
        5. The compiler will generate the assembly for the long `negate` program, that is not directly executable in VisUAL
        6. The file [`negate_gcc_8_2.S`](https://github.com/ivogeorg/cs2400-arm-asm-negate-exercise/blob/master/negate_gcc_8_2.S) contains the assembly ported to VisUAL
      - special attention on:
        1. Unsupported instructions (Just **Execute** on VisUAL and it will mark them)
           - in particular, `BX` is not supported, so you will need to use a new label or `MOV pc, rl` to return from a subroutine
        2. Memory regions (VisUAL only supports `DCD` and `FILL` directives)
        3. Start of execution (VisUAL starts executing the top line, so you might need to rearrange your code)
           - alternatively, you can define a `_start` label and load it into `pc`
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

