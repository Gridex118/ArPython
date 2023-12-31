# Instruction Set
### The machine uses 32 bit instructions, 6 bits of which are reserved for the opcodes

| OPCODE           | Mnemonic    | Binary   | Arguments                               | Scheme |
|------------------|-------------|----------|-----------------------------------------|--------|
| push             |  push       |  000000  | type(2 b)  data(24 b)                   | A1     |
| pop              |  pop        |  000001  | type(2 b)  to(24 b)                     | A2     |
| duplicate        |  dup        |  000010  |                                         |        |
| move             |  mov        |  000011  | type(4 b)  to(11 b)  from(11 b)         | B1     |
| addition         |  add        |  000100  | type(4 b)  to(4 b)  a(9/16 b)  b(9/16 b)| C      |
| substraction     |  sub        |  000101  | type(4 b)  to(4 b)  a(9/16 b)  b(9/16 b)| C      |
| multiplication   |  mul        |  000111  | type(4 b)  to(4 b)  a(9/16 b)  b(9/16 b)| C      |
| logic and        |  and        |  001000  | type(4 b)  to(4 b)  a(9/16 b)  b(9/16 b)| C      |
| logic or         |  or         |  001001  | type(4 b)  to(4 b)  a(9/16 b)  b(9/16 b)| C      |
| logic xor        |  xor        |  001010  | type(4 b)  to(4 b)  a(9/16 b)  b(9/16 b)| C      |
| logic not        |  not        |  001011  | type(2 b)  to(4 b)  a(20 b)             | D      |
| bit shift left   |  lsh        |  001100  | type(4 b)  to(4 b)  a(9/16 b)  b(9/16 b)| C      |
| bit shift right  |  rsh        |  001101  | type(4 b)  to(4 b)  a(9/16 b)  b(9/16 b)| C      |
| comparison       |  cmp        |  001110  | type(4 b)  a(11 b)  b(11 b)             | B2     |
| jump             |  jmp        |  001111  | cmp_type(3 b) dest_type(2 b)  to(21 b)  | E      |
| function call    |  call       |  010000  | dest_type(2 b)  to(24 b)                | A3     |
| print            |  print      |  010001  | undecided                               |        |
| write            |  write      |  010010  | undecided                               |        |
| halt             |  halt       |  010011  |                                         |        |

## Scheme A1
Types:
1. immediate
2. from register
3. from immediate memory address
4. from memory address stored in register

## Scheme A2
Types:
1. to void
2. to register
3. to immediate memory address
4. to memory add in register

## Scheme A3
Destination types:
1. immediate address
2. address stored in register

## Scheme B
Types:
1. from immediate to register
2. from immediate to immediate memory address
3. from immediate to memory address stored in register
4. from register to register
5. from register to immediate memory address
6. from register to memory address stored in register
7. from immediate memory address to register
8. from immediate memory address to immediate memory address
9. from memory address stored in register to register
10. from memory address stored in register to memory address stored in register

## Scheme C
Types:
1. immediate and register
2. immediate and immediate memory address
3. immediate and memory address stored in register
4. register and register
5. register and immediate memory address
6. register and memory address stored in register
7. immediate memory address and register
8. immediate memory address and immediate memory address
9. memory address stored in register and register
10. memory address stored in register and memory address stored in register
### Result can only be stored in a register
### If both *a* and *b* are zero, move to the next 32-word. *a* is the higher order 16-word and *b* the lower order 16-word

## Scheme E
Comparison types:
1. unconditionally
2. if equal
3. if less than
4. if greater than
5. if less than equal to
6. if greater than equal to  

Destination types:
1. to immediate address
2. to address stored in register


## Conversion example
### Python
```
numbers = (1, 2, 3, 4)
for number in numbers:
    print(number)
```

### Machine Mnemonics
```
        mov [numbers], 1
        mov [numbers + 1], 2
        mov [numbers + 2], 3
        mov [numbers + 3], 4
        mov Rbl, 0
for:    print int, [numbers + Rbl]
        add Rbl, Rbl, 1
        cmp Rbl, 3
        jmp ls for
        halt
```
