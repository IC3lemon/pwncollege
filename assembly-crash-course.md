
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

pwn.college{AHW04pE0RuTX-KXY5gDYFvTtUWZ.dBTM4MDL4UjM3QzW}
