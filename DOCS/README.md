# ArPython
A minimal bytecode type implementation of Python written in C

### This is just a hobby project; a not so seriously implemented approximation of the common CPython implementation.

## Minimum Features
- The basic primitives (lists, touples, numbers and strings)  
- Loops
- Conditionals
- Arithmatic and logical operators
- Functions  

## Nice to haves
- File importing  
- Classes
- Ternary operator
- Generators
- Unpacking
- Decorators

## Virtual Machine Specifications
This implementation uses a bytecode machine with four 32 bit general purpose registers, more about
which has been specified in [registers.md](./registers.md)  
Memory is implemented as two arrays of 8-bit cells, one for code and the other for data.  
The instruction set details have been specified in [instructions.md](./instructions.md).  
