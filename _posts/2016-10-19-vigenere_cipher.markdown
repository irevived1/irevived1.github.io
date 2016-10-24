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

Try it out on this [website](http://www.cs.du.edu/~snarayan/crypt/vigenere.html)!


**Breaking the Code**


Well, encryption is pretty boring.  Breaking some code would be much more exciting!  Thanks to some weird property of good o’ English.  The most frequently used letter is the letter ‘E’, and the next one is ‘T’ and so on:


![letterOfFreq](https://upload.wikimedia.org/wikipedia/commons/4/41/English-slf.png)

If we know the most frequently used letter in English will be E, then breaking Caesar Cipher is easy enough.  However, you would need a ciphered text with a good amount of sample.

Assuming in a ciphered text encrypted using Shift Cipher, the key is unknown.  You have counted the most frequently used letter is `K`.  We can save to assume that in this sample, E has converted into K.  

To unlock the mystery of the key, we’ll have to find the gap between K to E.

```
  A   B   C   D   E   F   G   H   I   J   K   L   M
 00  01  02  03  04  05  06  07  08  09  10  11  12


  N   O   P   Q   R   S   T   U   V   W   X   Y   Z
 13  14  15  16  17  18  19  20  21  22  23  24  25


K = 10, E = 04, the difference is 06 !  The key must be H
M = ( C -  N ) mod 26
M = (10 - 04 + 26 ) mod 26, M = 06  //adding 26 to prevent from going negative
```

Congratulations, you have found the key!
Cool, so we have learnt to decrypt Shift Cipher, what about Vigenere?
Well, if you think about it, Vigenere is just multiple Shift Ciphers joined together.  

```
CODINGISGREATILOVECODING
APPLEAPPLEAPPLEAPPLEAPPL
------------------------------


C    G    E    O    D        - encoded with A
 O    I    A    V    I       - encoded with P
  D    S    T    E    N      - encoded with P
   I    G    I    C    G     - encoded with L
    N    R    L    O         - encoded with E
```

Only if we can get the key length, and then break it into different bins and perform letter of frequency attack, then we can get the key for Vigenere!

Click [Here](https://vigenerecipher.herokuapp.com/vigenere.html)
