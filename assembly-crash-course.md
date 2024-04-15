
# `level-1`


### Challenge :



### Solution :

I directly tried using the method explained in the chal description, but I got this - \
![image](https://github.com/IC3lemon/pwncollege/assets/150153966/071c2516-836b-4735-ba7b-1bbf58b5d67a)

I looked it up. \
![image](https://github.com/IC3lemon/pwncollege/assets/150153966/65e1769c-68fc-48de-a34e-b019816855f5)

put the `%`, and this happened - \
![image](https://github.com/IC3lemon/pwncollege/assets/150153966/30fd8a6c-1860-432b-96ef-b19222a257ed)

A friend helped out tho (ASHWIN THE GOATT 🐐 🐐)

![image](https://github.com/IC3lemon/pwncollege/assets/150153966/64660fa5-58ce-41fd-8d92-4aaff4ec9610)

sure enough
```asm
.intel_syntax noprefix
mov %rdi, 0x1337
```
![image](https://github.com/IC3lemon/pwncollege/assets/150153966/b5a48451-4f7a-4cfd-970e-00aa1e6ffa62)


## flag > `pwn.college{Ird0_S-9a6HpZqspZkLxkLnMgwN.0FN5EDL4UjM3QzW}`


```
note - 

I looked up why exactly `.intel_syntax noprefix` worked. \
it was because the thing was probably using at&t syntax which is poo. \
I gotta specify what syntax to let the assembly use in the beginning.
```
<br><br><br>

***
<br><br><br>

# `level-2`


### Challenge :
```
Welcome to ASMLevel2
==================================================

To interact with any level you will send raw bytes over stdin to this program.
To efficiently solve these problems, first run it to see the challenge instructions.
Then craft, assemble, and pipe your bytes to this program.

For instance, if you write your assembly code in the file asm.S, you can assemble that to an object file:
  as -o asm.o asm.S

Note that if you want to use Intel syntax for x86 (which, of course, you do), you'll need to add the following to the start of asm.S:
  .intel_syntax noprefix

Then, you can copy the .text section (your code) to the file asm.bin:
  objcopy -O binary --only-section=.text asm.o asm.bin

And finally, send that to the challenge:
  cat ./asm.bin | /challenge/run

You can even run this as one command:
  as -o asm.o asm.S && objcopy -O binary --only-section=.text ./asm.o ./asm.bin && cat ./asm.bin | /challenge/run

In this level you will be working with registers. You will be asked to modify
or read from registers.



In this level you will work with multiple registers. Please set the following:
  rax = 0x1337
  r12 = 0xCAFED00D1337BEEF
  rsp = 0x31337
```

#### Solution :

I found insteresting shtuff : https://github.com/sidmittal32/pwn.college/tree/main/Assembly%20Crash%20Course

a wild forensics head spotted. \
I liked his approach of doing it via python scripts. \
I find python more comfier than assmebly. \
finna endorse this now. 

here's what I cooked :
```python
import pwn
pwn.context.update(arch="amd64")

code = pwn.asm("""
mov rax, 0x1337
mov r12, 0xCAFED00D1337BEEF
mov rsp, 0x31337
""")

process = pwn.process("/challenge/run")
process.write(code)

print(process.readall())
```

works like a charm : \
![image](https://github.com/IC3lemon/pwncollege/assets/150153966/060661d3-bdee-4cc0-8e70-e669e4fd69b0)


## flag > `pwn.college{AHW04pE0RuTX-KXY5gDYFvTtUWZ.dBTM4MDL4UjM3QzW}`
<br><br><br>

***
<br><br><br>

# `level-3`


### Challenge :
```
Welcome to ASMLevel3
==================================================

To interact with any level you will send raw bytes over stdin to this program.
To efficiently solve these problems, first run it to see the challenge instructions.
Then craft, assemble, and pipe your bytes to this program.

For instance, if you write your assembly code in the file asm.S, you can assemble that to an object file:
  as -o asm.o asm.S

Note that if you want to use Intel syntax for x86 (which, of course, you do), you'll need to add the following to the start of asm.S:
  .intel_syntax noprefix

Then, you can copy the .text section (your code) to the file asm.bin:
  objcopy -O binary --only-section=.text asm.o asm.bin

And finally, send that to the challenge:
  cat ./asm.bin | /challenge/run

You can even run this as one command:
  as -o asm.o asm.S && objcopy -O binary --only-section=.text ./asm.o ./asm.bin && cat ./asm.bin | /challenge/run

In this level you will be working with registers. You will be asked to modify
or read from registers.

We will now set some values in memory dynamically before each run. On each run
the values will change. This means you will need to do some type of formulaic
operation with registers. We will tell you which registers are set beforehand
and where you should put the result. In most cases, its rax.



Many instructions exist in x86 that allow you to do all the normal
math operations on registers and memory.

For shorthand, when we say A += B, it really means A = A + B.

Here are some useful instructions:
  add reg1, reg2       <=>     reg1 += reg2
  sub reg1, reg2       <=>     reg1 -= reg2
  imul reg1, reg2      <=>     reg1 *= reg2

div is more complicated and we will discuss it later.
Note: all 'regX' can be replaced by a constant or memory location

Do the following:
  add 0x331337 to rdi

We will now set the following in preparation for your code:
  rdi = 0x5ff
```

#### Solution :

pretty straight forward, add 0x331337 to rdi, put the result in rax. \
```python
import pwn
pwn.context.update(arch="amd64")

code = pwn.asm("""
add rdi, 0x331337
mov rax, rdi""")

process = pwn.process("/challenge/run")
process.write(code)
print(process.readall())
```
yay

![image](https://github.com/IC3lemon/pwncollege/assets/150153966/7b0e82ac-270a-495a-bdbe-221f842b5a7b)


## flag > `pwn.college{QgVVrFKwLV3rPYhaof2VsK0vMA_.0VN5EDL4UjM3QzW}`
<br><br><br>

***
<br><br><br>

# `level-4`


### Challenge :

```
Welcome to ASMLevel4
==================================================

To interact with any level you will send raw bytes over stdin to this program.
To efficiently solve these problems, first run it to see the challenge instructions.
Then craft, assemble, and pipe your bytes to this program.

For instance, if you write your assembly code in the file asm.S, you can assemble that to an object file:
  as -o asm.o asm.S

Note that if you want to use Intel syntax for x86 (which, of course, you do), you'll need to add the following to the start of asm.S:
  .intel_syntax noprefix

Then, you can copy the .text section (your code) to the file asm.bin:
  objcopy -O binary --only-section=.text asm.o asm.bin

And finally, send that to the challenge:
  cat ./asm.bin | /challenge/run

You can even run this as one command:
  as -o asm.o asm.S && objcopy -O binary --only-section=.text ./asm.o ./asm.bin && cat ./asm.bin | /challenge/run

In this level you will be working with registers. You will be asked to modify
or read from registers.

We will now set some values in memory dynamically before each run. On each run
the values will change. This means you will need to do some type of formulaic
operation with registers. We will tell you which registers are set beforehand
and where you should put the result. In most cases, its rax.



Using your new knowledge, please compute the following:
  f(x) = mx + b, where:
    m = rdi
    x = rsi
    b = rdx

Place the result into rax.

Note: there is an important difference between mul (unsigned
multiply) and imul (signed multiply) in terms of which
registers are used. Look at the documentation on these
instructions to see the difference.

In this case, you will want to use imul.

We will now set the following in preparation for your code:
  rdi = 0x22e7
  rsi = 0xd8
  rdx = 0x2578
```

### Solution :

Pretty straightforward yet again, mx + b \
m = rdi \
x = rsi \
b = rdx
and put the result in rax


```python
import pwn
pwn.context.update(arch="amd64")

code = pwn.asm("""
imul rdi, rsi
add rdx, rdi
mov rax, rdx
""")
process = pwn.process("/challenge/run")
process.write(code)
print(process.readall())
```

## flag > `pwn.college{MqxIl8upDgiCNTs0T2_nhrrFZRx.0lN5EDL4UjM3QzW}`

<br><br><br>
***
<br><br><br>

# `level-5`


### Challenge :

```
Welcome to ASMLevel5
==================================================

We will now set some values in memory dynamically before each run. On each run
the values will change. This means you will need to do some type of formulaic
operation with registers. We will tell you which registers are set beforehand
and where you should put the result. In most cases, its rax.

Division in x86 is more special than in normal math. Math in here is
called integer math. This means every value is a whole number.

As an example: 10 / 3 = 3 in integer math.

Why?

Because 3.33 is rounded down to an integer.

The relevant instructions for this level are:
  mov rax, reg1; div reg2

Note: div is a special instruction that can divide
a 128-bit dividend by a 64-bit divisor, while
storing both the quotient and the remainder, using only one register as an operand.

How does this complex div instruction work and operate on a
128-bit dividend (which is twice as large as a register)?

For the instruction: div reg, the following happens:
  rax = rdx:rax / reg
  rdx = remainder

rdx:rax means that rdx will be the upper 64-bits of
the 128-bit dividend and rax will be the lower 64-bits of the
128-bit dividend.

You must be careful about what is in rdx and rax before you call div.

Please compute the following:
  speed = distance / time, where:
    distance = rdi
    time = rsi
    speed = rax

Note that distance will be at most a 64-bit value, so rdx should be 0 when dividing.

We will now set the following in preparation for your code:
  rdi = 0x47c
  rsi = 0x5f

```

New stuff. main point of interest was this 
```asm
For the instruction: div reg, the following happens:
  rax = rdx:rax / reg
  rdx = remainder
```
```
rdx:rax means that rdx will be the upper 64-bits of
the 128-bit dividend and rax will be the lower 64-bits of the
128-bit dividend.
```

im guessing this is happens because all registers are 64 bit but div operation takes 128 bit divided \
so we use 2 64 bit registers to perform the thing.

```python
import pwn
pwn.context.update("arch64")

code = pwn.asm("""

""")
```
