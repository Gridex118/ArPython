# Instruction Set
### The machine uses 32 bit instructions, 6 bits of which are reserved for the opcodes

| OPCODE                  | Mnemonic    | Hex   | Arguments                               | Scheme |
|-------------------------|-------------|-------|-----------------------------------------|--------|
| push                    |  push       |  00h  | type(2 b)  data(24 b)                   | A1     |
| pop                     |  pop        |  01h  | type(2 b)  to(24 b)                     | A2     |
| duplicate               |  dup        |  02h  |                                         |        |
| move                    |  mov        |  03h  | type(4 b)  to(11 b)  from(11 b)         | B1     |
| addition                |  add        |  04h  | type(4 b)  to(4 b)  a(9/32 b)  b(9/32 b)| C      |
| substraction            |  sub        |  05h  | type(4 b)  to(4 b)  a(9/32 b)  b(9/32 b)| C      |
| multiplication          |  mul        |  06h  | type(4 b)  to(4 b)  a(9/32 b)  b(9/32 b)| C      |
| division                |  div        |  07h  | type(4 b)  to(4 b)  a(9/32 b)  b(9/32 b)| C      |
| logic and               |  and        |  08h  | type(4 b)  to(4 b)  a(9/32 b)  b(9/32 b)| C      |
| logic or                |  or         |  09h  | type(4 b)  to(4 b)  a(9/32 b)  b(9/32 b)| C      |
| logic xor               |  xor        |  0Ah  | type(4 b)  to(4 b)  a(9/32 b)  b(9/32 b)| C      |
| logic not               |  not        |  0Bh  | type(2 b)  to(4 b)  a(20 b)             | D      |
| bit shift left          |  lsh        |  0Ch  | type(4 b)  to(4 b)  a(9/32 b)  b(9/32 b)| C      |
| bit shift right         |  rsh        |  0Dh  | type(4 b)  to(4 b)  a(9/32 b)  b(9/32 b)| C      |
| comparison              |  cmp        |  0Eh  | type(4 b)  a(11 b)  b(11 b)             | B2     |
| jump                    |  jmp        |  0Fh  | type(2 b)  to(24 b)                     | A3     |
| jump if equal to        |  jeq        |  10h  | type(2 b)  to(24 b)                     | A3     |
| jump if not equal to    |  jneq       |  11h  | type(2 b)  to(24 b)                     | A3     |
| jump if less than       |  jls        |  12h  | type(2 b)  to(24 b)                     | A3     |
| jump if greater than    |  jgr        |  13h  | type(2 b)  to(24 b)                     | A3     |
| jump if less or eql     |  jle        |  14h  | type(2 b)  to(24 b)                     | A3     |
| jump if greater or eql  |  jge        |  15h  | type(2 b)  to(24 b)                     | A3     |
| function call           |  call       |  16h  | type(2 b)  to(24 b)                     | A3     |
| return from function    |  ret        |  17h  |                                         |        |
| print                   |  print      |  18h  | from(2 b)  data_type(2 b)  data(24 b)   | E      |
| write                   |  write      |  19h  | from(2 b)  data_type(2 b)  data(24 b)   | E      |
| halt                    |  halt       |  1Ah  |                                         |        |

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
2. address stored in memory address
3. address stored in register

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
### If both *a* and *b* are zero, the next 32-word is *a* and the one after that is *b*

## Scheme D
Type:
1. immediate
2. immediate memory address
3. memory address in register
4. register

## Scheme E
From:
1. from immediate memory address
2. from memory address in register
3. from register

Data Type:
1. number
2. string
3. escape sequence


## Conversion example
### Python
```
numbers = (1, 2, 3, 4)
for number in numbers:
    print(number)
```

### Machine Mnemonics
```
        mov [64h], 1                ; the first element in numbers is stored at memory address 64h
        mov [64h + 1], 2
        mov [64h + 2], 3
        mov [64h + 3], 4
        mov Rbl, 0
for:    print int, [64h + Rbl]
        add Rbl, Rbl, 1
        cmp Rbl, 3
        jls for
        halt
```
