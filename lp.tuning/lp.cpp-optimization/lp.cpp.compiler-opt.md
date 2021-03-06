
# C++ Optimization Strategies and Techniques

- [GNU Compiler Optimization](https://gcc.gnu.org/onlinedocs/gcc/Optimize-Options.html)
- [GNU Link time optimizations](https://gcc.gnu.org/wiki/LinkTimeOptimization#:~:text=10%2Fmsg00060.html-,Background,optimized%20as%20a%20single%20module)

```
- Need for the speed
        - Time your code performance manually			
        - Use source code instrumentation to measure code execution time				
        - Use the perf tool to analyze program performance
        - Use the godbolt compiler explorer tool to analyze machine code generated by a compiler
        - Use compiler flags to generate better code
        - Apply code idioms that result in performance
        - Write cache-friendly code		
        - Apply algorithm-level optimizations to real-world problems

- Performance Measurement			
        - The most important aspect of optimization is the measurement of code execution time. 
        - Unless we measure our application's performance with a wide range of input datasets, 
        - we will have no clue as to which part takes the most time and,
        - our optimization efforts will be shot in the dark, with no guarantee of a result. 
            - There are several approaches for measurement, and some of them are listed here:			
                - Runtime instrumentation or profiling	
                - Source code instrumentation	
                - Manual execution timing				
                - Studying generated assembly code	
                 - Manual estimation by studying the code and algorithms used

                 

- Optimization Strategies

        - Compiler-based optimization				
        - Source code micro-optimization
        - Cache-friendly code
        - Algorithmic optimization
        - Link Time Optimi[zs]ation
            - LTO grants the compiler the opportunity to see more than a single .o file at a time. 
                This grants extra freedom for the optimisation that yields:
                    - reduced code size (seen binaries down to 40%, but expect some 5-20% reduction)
                    - increased execution speed (hey, there is less code for the same thing, 
                    how much faster depends on how the application, obviously)
                    - Add -flto CFLAGS and/or CXXFLAGS depending
                    - Add all CFLAGS/CXXFLAGS to LDFLAGS, including the -flto
                    - Redirect linker, ranlib and ar


- OPTIMIZATION FOR BRANCH PREDICTION
- LOOP UNROLLING
- OPTIMIZING LOGICAL OPERATORS
- USING THE STD::VECTOR CONTAINER EFFICIENTLY
- PROFILE GUIDED OPTIMIZATION
- USING COMPILER PARALLELIZATION 




- C++ Design Considerations
    - Take advantage of STL containers
    - Consider using references instead of pointers
    - Consider two-phase construction
    - Limit exception handling
    - Avoid Runtime Type Identification
    - Prefer stdio to iostream
    - Evaluate alternative libraries

- 
    - Pass class parameters by reference
    - Postpone variable declaration as long as possible
    - Prefer initialization over assignment
    - Use constructor initialization lists
    - Prefer operator= over operator alone
    - Use prefix operators
    - Use explicit constructors

- Final Aoptimization
    - Your app is up and running. The data structures are ideal, the algorithms sublime, the code elegant, 
      but the program - well, it's not quite living up to its potential. 
    - Time to get drastic, and with drastic measures, there are tradeoffs to consider. 
    - These optimizations are going to make your code less modular, harder to understand, and more difficult to maintain. 
      They may cause unexpected side effects like code bloat. 
    - Your compiler may not even be able to handle some of the more advanced template-based techniques. 
       Proceed with caution. Arm yourself with a good profiler.
       
        - Inline functions
        - Avoid temporary objects: the return value optimization
        - Be aware of the cost of virtual functions
        - Return objects via reference parameters
        - Consider per-class allocation
        - Consider STL container allocators
        - The "empty member" optimization
        - Template metaprogramming
        - Copy on write



 - Compiler Optimizations
    -O0 or no -O option (default)
       - At this optimization level GCC does not perform any optimization  
       - compiles the source code in the most straightforward way possible 
         Each command in the source code is converted directly to the corresponding instructions in the executable file,
         without rearrangement. 
       - This is the best option to use when debugging a program and is the default if 
         no optimization level option is specified.
    -O1 or -O
        - This level turns on the most common forms of optimization that do not require any speed-space tradeoffs. 
        - With this option the resulting executables should be smaller and faster than with -O0. 
        - The more expensive optimizations, such as instruction scheduling, are not used at this level.
        - Compiling with the option -O1 can often take less time than compiling with -O0, due to the reduced amounts of data that need to be processed after simple optimizations.
    -O2
        - This option turns on further optimizations, in addition to those used by -O1. 
        - These additional optimizations include instruction scheduling. 
        - Only optimizations that do not require any speed-space tradeoffs are used,
        - so the executable should not increase in size. 
        - The compiler will take longer to compile programs and require more memory than with -O1. 
        - This option is generally the best choice for deployment of a program, because it provides maximum optimization without   increasing the executable size. It is the default optimization level for releases of GNU packages.
    -O3
        - This option turns on more expensive optimizations, such as function inlining, in addition to all the optimizations of the lower levels -O2 and -O1. 
        - The -O3 optimization level may increase the speed of the resulting executable, but can also increase its size. 
          Under some circumstances where these optimizations are not favorable, this option might actually make a program slower.
    -funroll-loops
        - This option turns on loop-unrolling, and is independent of the other optimization options. 
        - It will increase the size of an executable.
        -  Whether or not this option produces a beneficial result has to be examined on a case-by-case basis.
    -Os
        - This option selects optimizations which reduce the size of an executable. 
        - The aim of this option is to produce the smallest possible executable, 
          for systems constrained by memory or disk space. 
          In some cases a smaller executable will also run faster, due to better cache usage.
    
```  
    
   [gcc compiler ops](https://caiorss.github.io/C-Cpp-Notes/compiler-flags-options.html)