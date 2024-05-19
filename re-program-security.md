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

# level 2.1
