---
layout: post
title:  "Vigenere Cipher"
date:   2016-10-19 11:00:00 -0400
---

10.19.16

Vigenere Cipher

Understanding Shift Cipher is crucial before jumping into Vigenere Cipher.  The Caesar cipher, also known as a shift cipher, is one of the simplest forms of encryption. It is a substitution cipher where each letter in the original message is replaced with a letter corresponding to a certain number of letters up or down in the alphabet.  Like so:


![Shift cipher](https://people.rit.edu/~epa4566/140/project3/images/ezgif-save.gif)


You simply align the alphabets, shift the text to one direction and match the letters from top to bottom to get the ciphered text.  To decrypt the message, you would do the same thing, but this time, you would shift it to the opposite direction.


To encrypt or decrypt letters mathematically, we can use the following equation:


Shift = N
```
C = (M + N) mod 26
```
Decryption is performed similarly,
```
M = (C - N) mod 26
```
Giving the following where A is at index of 0 and Z is at index of 25:


```
  A   B   C   D   E   F   G   H   I   J   K   L   M
 00  01  02  03  04  05  06  07  08  09  10  11  12


  N   O   P   Q   R   S   T   U   V   W   X   Y   Z
 13  14  15  16  17  18  19  20  21  22  23  24  25


Encryption Example with N = 3, or with KEY ‘D’:
MESSAGE = APPLE
        C = ( M + N ) mod 26
A = 00, C = (00 + 3 ) mod 26,   C = 03 =   D
P = 15, C = (15 + 3 ) mod 26,   C = 18 =   S
P = 15, C = (15 + 3 ) mod 26,   C = 18 =   S
L = 11, C = (11 + 3 ) mod 26,   C = 14 =   O
E = 04, C = (04 + 3 ) mod 26,   C = 07 =   H


CIPHERED TEXT: DSSOH
```


Similarly for decryption:


```
Decryption Example with N = 3, or with KEY ‘D’:
MESSAGE = DSSOH
        M = ( C - N ) mod 26
D = 03, M = (03 - 3 ) mod 26,   M = 00 =   A
S = 18, M = (18 - 3 ) mod 26,   M = 15 =   P
S = 18, M = (18 - 3 ) mod 26,   M = 15 =   P
O = 14, M = (14 - 3 ) mod 26,   M = 11 =   l
H = 07, M = (07 - 3 ) mod 26,   M = 04 =   E


RESULT = APPLE


```
Or do it in one shot


```
APPLE
DDDDD
-----
DSSOH
```

Vigenere Cipher is no different than Shift Cipher, but on a steroid.  

![Vigenere Cipher](https://people.rit.edu/~epa4566/140/project3/media/vigSmall.gif)

```
CODING IS GREAT, I LOVE CODING
APPLEA PP LEAPP  L EAPP LEAPPL
------------------------------
CDSTRG XH RVEPI, T POKT NSDXCR
```

Notice how in Vigenere Cipher, the key just repeats itself until the end of the input.  Whereas in Shift Cipher, the key is only one letter.



Click [Here](https://vigenerecipher.herokuapp.com/vigenere.html)
