# level-1.0

### Challenge : 

```
###
### Welcome to ./babyrev_level1.0!
###

This license verifier software will allow you to read the flag. However, before you can do so, you must verify that you
are licensed to read flag files! This program consumes a license key over stdin. Each program may perform entirely
different operations on that input! You must figure out (by reverse engineering this program) what that license key is.
Providing the correct license key will net you the flag!

```

### Solution :

On opening with IDA, in main, saw the variable `EXPECTED_RESULT`
![image](https://github.com/IC3lemon/pwncollege/assets/150153966/10e7769f-ce68-483e-af26-4da9b133dda1)

and that was it.
![image](https://github.com/IC3lemon/pwncollege/assets/150153966/4da3cc72-b6ee-4647-a9bb-12472b7622f2)

## flag > `pwn.college{kzfHoyIzFlCU3LbrcpHrgueATDD.0VM1IDL4UjM3QzW}`

***

# level 1.1

### Challenge : 

```
same thing as 1.0
```

### Solution : 

opened with IDA, saw that it was being checked with a variable 
![image](https://github.com/IC3lemon/pwncollege/assets/150153966/0443ede1-02ae-4785-8a75-c57cf94e1129)

## flag > `pwn.college{0kv69lrydFlqYO4EH5Z8PZhIYF3.0lM1IDL4UjM3QzW}`

***

# level 2.0

### Challenge :

```
Reverse engineer this challenge to find the correct license key, but your input will be modified somehow before being compared to the correct key.
```

### Solution : 

![image](https://github.com/IC3lemon/pwncollege/assets/150153966/179266fc-0898-4f79-94b6-4a9cf930d28b)

![image](https://github.com/IC3lemon/pwncollege/assets/150153966/2d2ab886-e8de-4c5e-9387-5a085e4f0e3b)

so just swap 0, 2
`faasx`

![image](https://github.com/IC3lemon/pwncollege/assets/150153966/508575cc-9dd2-4b53-a083-21d39dc18af3)

## flag > `pwn.college{w4kg1vNGUXbBcdUYTVIJBIhyNyw.01M1IDL4UjM3QzW}`

***

```
level 2.1 - level 7.0 were similar and just needed to be backtraced through the operations to get the key.
therefore, I am not documenting these to save time.
```

***

# level 7.1

### Challenge :

```
Reverse engineer this challenge to find the correct license key, but your input will be modified somehow before being compared to the correct key.
```

### Solution : 

what I think was happening :
```
1. an xor with 0x15CA
2. reverses string 3 times.. i.e. 1 reversal
3. sorting
```

was stuck on this for hours, I followed the earlier procedure of backtracking from the expected output \
but that was not working, simply because \
the sort. 

because the sort, the order in which items got xor's was lost. \
and since u can't undo a sort I was feeling pretty stuck. \
on backtracking the key I was getting was unreadable. unlike the previous challs. \
fortunately for our lord and saviour akaash 

![image](https://github.com/IC3lemon/pwncollege/assets/150153966/b7c1f533-8ace-4d10-a194-5a472f0ff303)

basically how he solved this was..
he xor'd each character with `0x15` and `0xCA` to see if he got readable characters. \
and bro noticed a pattern. \
![image](https://github.com/IC3lemon/pwncollege/assets/150153966/69c0b9f0-ac0c-4636-8931-65171560e983)

and to the answer to his question
![image](https://github.com/IC3lemon/pwncollege/assets/150153966/7e5cd168-8b23-4430-b19f-eb71a0701f85)

so basically, the sort sorted the `0xCA` xord characters into the second half. \
because xoring with `0xCA` adds an 8th bit, making it numerically larger than the others. 

![image](https://github.com/IC3lemon/pwncollege/assets/150153966/e1407e2c-ea86-40f1-9de7-a4eccfd01545)

***

# level 9.0

### Challenge :

```
Reverse engineer this challenge to find the correct license key, but your input will be modified somehow before being compared to the correct key. This challenge allows you to patch 5 bytes in the binary.
```

### Solution :

here the input was being hashed and then compared to a hash. \
being a good crypto boi. I know that one cannot crack hashes. \
well it is possible but it would take years. 

So I realised what I had to do here was not backtrtack like earlier challs, but modify the binary to allow me to get to the end, regardless of my input. \

first of all I looked up how to patch binaries.
I ended up on this vid : https://www.youtube.com/watch?v=LyNyf3UM9Yc
and I realised, I should prolly do exactly what this guy is doing.

This guy was changing the check. \
the check was happening to compare with a value, if equal, it lets u pass. \
I realised I gotta do the same, I gotta change the jnz to a jz.

on opening my binary in ida I saw this. \
![image](https://github.com/IC3lemon/pwncollege/assets/150153966/98928198-8c3d-4cc3-812d-c033fd759d9e)

This was what I had to mess with. \
It seems the win condition would only be called if the jnz here were a jz.

Taking a look at the hex, 
![image](https://github.com/IC3lemon/pwncollege/assets/150153966/3db32b1c-9170-4833-94c4-da746c41c694)

we can see the bytes 75 at `246A` and 14 at `246B` \
basically, the 75 represents the jnz and 0x14 is the offset from its current address that it should jump to when the condition is true. 

so to make it a jz we have to change it from 75 to 74.

I have the address `246A` and I have the byte to change it to `74`.

on running the program, I realised we could change 4 other bytes, but that was worthless, this one change should do the trick. \
so I just spammed 0 0 0 0  for the other 4.

![image](https://github.com/IC3lemon/pwncollege/assets/150153966/876ac293-c00e-49a0-b8a9-7d40454ad3cd)

and yes

![image](https://github.com/IC3lemon/pwncollege/assets/150153966/fc84ef99-0a58-4e27-80b5-551cf2f9e6f6)

***

```
level 9.1, 10.0, 10.1 were the same, just had to figure out the address of the check and set the value to 75-1
```
***

# level 11.0

### Challenge :

```
Reverse engineer this challenge to find the correct license key, but your input will be modified somehow before being compared to the correct key. This challenge allows you to patch 2 bytes in the binary, but performs an integrity check afterwards.
```

### Solution :

So two checks would be there. \
one where it checks the recieved license key. \
another where it checks integrity

And we are also allowed to patch 2 bytes. \
so basically, bypass both the checks.

the license key check :
![image](https://github.com/IC3lemon/pwncollege/assets/150153966/e9fc3746-a0e7-4f2a-b7f0-1f7361d0349b)


the integrity check :
![image](https://github.com/IC3lemon/pwncollege/assets/150153966/f47a51e6-e339-4649-876d-2ad459d66281)

and yes.

![image](https://github.com/IC3lemon/pwncollege/assets/150153966/ee83fb19-6d1b-4ded-9c1a-e992b7133e0c)

![image](https://github.com/IC3lemon/pwncollege/assets/150153966/3470d36d-24af-4722-a105-bc2b707f0791)



