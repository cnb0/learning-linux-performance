# Valgrind HOWTO and Examples


```

- Valgrind is a memory mismanagement detector.
  It shows you memory leaks, deallocation errors, etc.
- Actually, Valgrind is a wrapper around a collection of tools that do many other things (e.g., cache profiling); 
   Memcheck can detect:
		- Use of uninitialised memory
		- Reading/writing memory after it has been free'd
		- Reading/writing off the end of malloc'd blocks
		- Reading/writing inappropriate areas on the stack
		- Memory leaks -- where pointers to malloc'd blocks are lost forever
		- Mismatched use of malloc/new/new [] vs free/delete/delete []
		- Overlapping src and dst pointers in memcpy() and related functions
		- Some misuses of the POSIX pthreads API

- This repository contains several examples of Valgrind Memcheck usage. 

-  Valgrind sometimes gets things wrong and generates false-positives. 
   To suppress the warnings about those, Valgrind uses `suppression files`. In
   this repository, those are named with a `.sup` extension and live in `test/`
   directory.


valgrind --leak-check=full \
         --show-leak-kinds=all \
         --track-origins=yes \
         --verbose \
         --log-file=valgrind-out.txt \
         ./executable exampleParam1
The flags are, in short:

--leak-check=full: "each individual leak will be shown in detail"
--show-leak-kinds=all: Show all of "definite, indirect, possible, reachable" leak kinds in the "full" report.
--track-origins=yes: Favor useful output over speed. 
  This tracks the origins of uninitialized values, which could be very useful for memory errors. 
  Consider turning off if Valgrind is unacceptably slow.
--verbose: Can tell you about unusual behavior of your program. Repeat for more verbosity.
--log-file: Write to a file. Useful when output exceeds terminal space.
```

Techniques for Debugging Memory Leaks & Errors

```
	     - Invalid write
		 - Invalid read

		- General advice for memory leaks:
			Make sure your dynamically allocated memory does in fact get freed.
			Don't allocate memory and forget to assign the pointer.
			Don't overwrite a pointer with a new one unless the old memory is freed.
		- General advice for memory errors:
			    Access and write to addresses and indices you're sure belong to you. 
			    Memory errors are different from leaks; they're often just 
			    IndexOutOfBoundsException type problems.
			    Don't access or write to memory after freeing it.
		- Sometimes your leaks/errors can be linked to one another, much like 
		  an IDE discovering that you haven't typed a closing bracket yet. 
		  Resolving one issue can resolve others, so look for one that looks a 
		  good culprit and apply some of these ideas:
		    - List out the functions in your code that depend on/are dependent on the "offending" 
		      code that has the memory error. 
		      Follow the program's execution (maybe even in gdb  perhaps), and 
		      look for precondition/postcondition errors. 
		     The idea is to trace your program's execution while focusing on the lifetime of allocated memory.
		   - Try commenting out the "offending" block of code (within reason, so your code still compiles). 
		     If the Valgrind error goes away, you've found where it is.


# How to build sample programs

Just type make:

	make

You'll get a lot of programs named with `.prog` extension. Sample output:

~~~terminal
gcc -Wall -pedantic -std=c99 -g -ggdb -O0 empty.c -o empty 
gcc -Wall -pedantic -std=c99 -g -ggdb -O0 fscanf.c -o fscanf 
gcc -Wall -pedantic -std=c99 -g -ggdb -O0 fscanf_many.c -o fscanf_many
gcc -Wall -pedantic -std=c99 -g -ggdb -O0 printf.c -o printf
gcc -Wall -pedantic -std=c99 -g -ggdb -O0 vprintf_warn.c -o vprintf_warn
~~~

You can run each `.prog` file and see its result.


# How to run Valgrind checking for memory leaks

Just tyoe:

	make check

Sample output:

~~~terminal
valgrind -v --tool=memcheck --gen-suppressions=all --suppressions=data/empty.memcheck.sup --log-file=empty.memcheck --track-origins=yes ./empty 
valgrind -v --tool=memcheck --gen-suppressions=all --suppressions=data/fscanf.memcheck.sup --log-file=fscanf.memcheck --track-origins=yes ./fscanf 
valgrind -v --tool=memcheck --gen-suppressions=all --suppressions=data/fscanf_many.memcheck.sup --log-file=fscanf_many.memcheck --track-origins=yes ./fscanf_many
valgrind -v --tool=memcheck --gen-suppressions=all --suppressions=data/printf.memcheck.sup --log-file=printf.memcheck --track-origins=yes ./printf
tab_size: 20
valgrind -v --tool=memcheck --gen-suppressions=all --suppressions=data/vprintf_warn.memcheck.sup --log-file=vprintf_warn.memcheck --track-origins=yes ./vprintf_warn
Going to read: 1 elements
~~~

Output sits in `.memcheck` files. They have a Valgrind output. Passed flags
mean verbose output (`-v`), use default Memcheck tool (`--tool=memcheck`),
generate suppressions without asking (`--gen-suppressions=all`), use not
only default, but also additional suppression file (`--suppressions`) log
output to the file (`--log-file`) and in case of memory problems, show
exactly where they're coming from (`--track-origin`). 


