---
layout: post
title:  "RSA Key Exchange Algorithm"
date:   2016-08-29 16:54:20 -0400
---


08.29.2016

RSA Key Exchange Algorithm

**RSA**, designed by Ron Rivest, Adi Shamir, and Leonard Adleman in 1977, is one of the first practical public-key cryptosystems and is widely used for secure data transmission.  It is extremely difficult to factor the product of two large prime numbers and RSA took advantage of this mathematical property and made it into an asymmetric cryptographic algorithm.  

Today, I am not going to talk about the history or the background of RSA, nor the practicality of the algorithm itself.  Instead, we will be talking about the pure mathematical aspects of RSA, and maybe we’ll build some Ruby methods to clarify some of the key points as well.

Before diving deep into RSA, it is very important to understand a few key concepts:

 - What is a common denominator.
 - What is greatest common divisor.
 - What is a prime number.
 - What does it mean to be relatively prime to a number.
 - Power modular arithmetic. 
 - Inverse modular arithmetic.


**Common Denominator:** Mathematics. a number that is a multiple of all the denominators of a set of fractions.
 *For Example:* 18 and 12, common denominators are: 6,3,2

**Greatest Common Divisor:** is the largest positive integer that divides the numbers without a remainder.
 *For Example:* 18 and 12, the greatest common divisor is 6

<pre ><span style="color:#aeaeae;font-style:italic">#simple method to find the GCD using The Euclidean Algorithm</span>
<span style="color:#aeaeae;font-style:italic">#GCD method</span>
<span style="color:#e28964">def</span> <span style="color:#89bdff">gcd</span>(<span style="color:#3e87e3">a,b</span>)
  <span style="color:#e28964">return</span> b <span style="color:#e28964">if</span> a<span style="color:#e28964">==</span><span style="color:#3387cc">0</span>
  <span style="color:#e28964">return</span> gcd(b<span style="color:#e28964">%</span>a,a)
<span style="color:#e28964">end</span>
</pre>



**Prime number:** A prime number (or a prime) is a natural number greater than 1 that has no positive divisors other than 1 and itself.

*To verify whether a number is prime, you only need to check from 2 to square root of that particular number.  If there aren’t any within the range that can be divided with the remainder of 0, then the number is a prime.*

<pre ><span style="color:#aeaeae;font-style:italic">#A simple and slow prime method to find the next prime of a number</span>
<span style="color:#aeaeae;font-style:italic">#random prime generator</span>
<span style="color:#e28964">def</span> <span style="color:#89bdff">primeGen</span>(<span style="color:#3e87e3">num</span>)
  <span style="color:#e28964">loop</span> <span style="color:#e28964">do</span>
    <span style="color:#e28964">if</span> num<span style="color:#e28964">%</span><span style="color:#3387cc">2</span><span style="color:#e28964">==</span><span style="color:#3387cc">0</span>
      num <span style="color:#e28964">+=</span> <span style="color:#3387cc">1</span>
      <span style="color:#e28964">next</span>
    <span style="color:#e28964">elsif</span> num<span style="color:#e28964">%</span><span style="color:#3387cc">3</span><span style="color:#e28964">==</span><span style="color:#3387cc">0</span> <span style="color:#e28964">||</span> num<span style="color:#e28964">%</span><span style="color:#3387cc">5</span><span style="color:#e28964">==</span><span style="color:#3387cc">0</span>
      num <span style="color:#e28964">+=</span> <span style="color:#3387cc">2</span>
      <span style="color:#e28964">next</span>
    <span style="color:#e28964">else</span>
      <span style="color:#e28964">return</span> num <span style="color:#e28964">if</span> <span style="color:#9b859d">Prime</span>.prime?(num)
      num <span style="color:#e28964">+=</span> <span style="color:#3387cc">1</span>
    <span style="color:#e28964">end</span>
  <span style="color:#e28964">end</span>
<span style="color:#e28964">end</span>
</pre>


**Co-prime:** This one is a little bit tricky, is two integers a and b are said to be relatively prime, mutually prime, if the only positive integer that divides both of them is 1.
*For example:* 1,3,5,7 are coprimes of 8. Where as 1,2,4,5,7,8 are coprimes of 9

An interesting property for prime numbers: The number of coprimes for prime numbers will be the prime number - 1
For example, [1,2,3,4] are coprimes of 5 and [1,2,3,4,5,6] are coprimes 7

<pre ><span style="color:#aeaeae;font-style:italic">#here’s a ruby method to randomly pick a coprime from a given input</span>
<span style="color:#e28964">def</span> <span style="color:#89bdff">get_E</span>(<span style="color:#3e87e3">limit</span>)
  lower <span style="color:#e28964">=</span> limit <span style="color:#e28964">>></span> <span style="color:#3387cc">1</span>
  <span style="color:#e28964">loop</span> <span style="color:#e28964">do</span>
    e <span style="color:#e28964">=</span> rand(lower..limit)
    <span style="color:#e28964">return</span> e <span style="color:#e28964">if</span> (gcd(e,limit)<span style="color:#e28964">==</span><span style="color:#3387cc">1</span>)
  <span style="color:#e28964">end</span>
<span style="color:#e28964">end</span>

</pre>


**Power Modular Arithmetic:**
This arithmetic comes in the form of (b^e)%n, the result will always be less than n.
Without the proper algorithm, this arithmetic will have the potential to overflow the variable.

<pre ><span style="color:#aeaeae;font-style:italic">#power mod method</span>
<span style="color:#e28964">def</span> <span style="color:#89bdff">power_mod</span>(<span style="color:#3e87e3">base,exp,mod</span>)
  result <span style="color:#e28964">=</span> <span style="color:#3387cc">1</span>
  <span style="color:#e28964">while</span> ( exp <span style="color:#e28964">></span> <span style="color:#3387cc">0</span> )
    ( result <span style="color:#e28964">=</span> (result <span style="color:#e28964">*</span> base) <span style="color:#e28964">%</span> mod ) <span style="color:#e28964">if</span> exp <span style="color:#e28964">%</span> <span style="color:#3387cc">2</span> <span style="color:#e28964">==</span> <span style="color:#3387cc">1</span>
    exp <span style="color:#e28964">=</span> exp <span style="color:#e28964">>></span> <span style="color:#3387cc">1</span>
    base <span style="color:#e28964">=</span> (base<span style="color:#e28964">*</span>base) <span style="color:#e28964">%</span> mod
  <span style="color:#e28964">end</span>
  <span style="color:#e28964">return</span> result
<span style="color:#e28964">end</span>

</pre>


Lastly, the **Inverse modular arithmetic.** The Inverse modular arithmetic can be expressed by the following equation:

 # ax + by = gcd(a, b)

A well known method to solve the modular multiplicative inverse is to use extended Euclidean algorithm.
[https://en.wikipedia.org/wiki/Extended_Euclidean_algorithm](http://)

We know that in RSA, we will be dealing with finding the inverse mod of two numbers that are relatively prime, in this case, the section for gcd(a,b) can be simplified to 1:
 # ax + by = 1

We need to find x where x is a positive number.

This method can be a little bit difficult to code so I grabbed [https://rosettacode.org/](http://) for help:

<pre ><span style="color:#aeaeae;font-style:italic"># inverse mod function obtained from https://rosettacode.org/wiki/Modular_inverse#Ruby</span>
<span style="color:#e28964">def</span> <span style="color:#89bdff">extended_gcd</span>(<span style="color:#3e87e3">a, b</span>)
  last_remainder, remainder <span style="color:#e28964">=</span> a.abs, b.abs
  x, last_x, y, last_y <span style="color:#e28964">=</span> <span style="color:#3387cc">0</span>, <span style="color:#3387cc">1</span>, <span style="color:#3387cc">1</span>, <span style="color:#3387cc">0</span>
  <span style="color:#e28964">while</span> remainder <span style="color:#e28964">!=</span> <span style="color:#3387cc">0</span>
    last_remainder, (quotient, remainder) <span style="color:#e28964">=</span> remainder, last_remainder.divmod(remainder)
    x, last_x <span style="color:#e28964">=</span> last_x <span style="color:#e28964">-</span> quotient<span style="color:#e28964">*</span>x, x
    y, last_y <span style="color:#e28964">=</span> last_y <span style="color:#e28964">-</span> quotient<span style="color:#e28964">*</span>y, y
  <span style="color:#e28964">end</span>

  <span style="color:#e28964">return</span> last_remainder, last_x <span style="color:#e28964">*</span> (a <span style="color:#e28964">&lt;</span> <span style="color:#3387cc">0</span> <span style="color:#e28964">?</span> <span style="color:#e28964">-</span><span style="color:#3387cc">1</span> : <span style="color:#3387cc">1</span>)
<span style="color:#e28964">end</span>

<span style="color:#e28964">def</span> <span style="color:#89bdff">invmod</span>(<span style="color:#3e87e3">e, et</span>)
  g, x <span style="color:#e28964">=</span> extended_gcd(e, et)
  <span style="color:#e28964">if</span> g <span style="color:#e28964">!=</span> <span style="color:#3387cc">1</span>
    <span style="color:#e28964">raise</span> <span style="color:#65b042">'The maths are broken!'</span>
  <span style="color:#e28964">end</span>
  x <span style="color:#e28964">%</span> et
<span style="color:#e28964">end</span>
</pre>


# That took a while to explain what’s required to understand RSA.


Let’s use the methods above to demonstrate it, don’t forget to put **<span style="color:#e28964">require</span> <span style="color:#65b042">'prime'</span>** on top of your ruby file.

**In a parallel world, Alice has a password that wants to send to Bob.  Bob will start to generate some numbers and will send some public keys to Alice.**

<pre ><span style="color:#aeaeae;font-style:italic">#that’s the range for the random generator</span>
range <span style="color:#e28964">=</span> (<span style="color:#3387cc">99999999</span>..<span style="color:#3387cc">999999999</span>)
p <span style="color:#e28964">=</span> primeGen(rand(range))
q <span style="color:#e28964">=</span> primeGen(rand(range))

puts <span style="color:#65b042">"Random P: <span style="color:#daefa3">#{p}</span>"</span>
puts <span style="color:#65b042">"Random Q: <span style="color:#daefa3">#{q}</span>"</span>
</pre>

**Bob will have to generate two prime numbers, called *p* and *q*,**
**N will be the product of P and Q**


<pre >n <span style="color:#e28964">=</span> p<span style="color:#e28964">*</span>q
puts <span style="color:#65b042">"N = <span style="color:#daefa3">#{n}</span>"</span>
</pre>

**PHI is the number of coprimes in N, if p has p-1 coprimes and q has q-1 coprimes, the number of coprimes for will be (p-1)*(q-1)**

<pre >phi <span style="color:#e28964">=</span> (p<span style="color:#e28964">-</span><span style="color:#3387cc">1</span>)<span style="color:#e28964">*</span>(q<span style="color:#e28964">-</span><span style="color:#3387cc">1</span>)
puts <span style="color:#65b042">"PHI: <span style="color:#daefa3">#{phi}</span>"</span>

</pre>

**E is a number that is relatively prime to PHI**

<pre >e <span style="color:#e28964">=</span> get_E(phi)
puts <span style="color:#65b042">"The chosen E: <span style="color:#daefa3">#{e}</span>"</span>
</pre>

**Finally, D is the inverse mod of E and PHI.**

<pre >d <span style="color:#e28964">=</span> invmod(e,phi)
puts <span style="color:#65b042">"D = <span style="color:#daefa3">#{d}</span>"</span>
</pre>

**Then Bob sends the public keys to Alice, which is N and E**

**Alice receives N and E and proceeds to encrypt**

<pre >puts <span style="color:#65b042">"<span style="color:#ddf2a4">\n</span>Bob sends N and E to Alice."</span>
</pre>

**Alice wants to send *12345678* to Bob.**

<pre >m <span style="color:#e28964">=</span> <span style="color:#3387cc">12345678</span>
puts <span style="color:#65b042">"Alice wants to send this message to Bob: <span style="color:#daefa3">#{m}</span>"</span>
</pre>

**Alice encrypts the password using the power mod, m^e mod N and sends the cipher message to Bob**.

<pre >puts <span style="color:#65b042">"Alice uses E and N to encrypt the message."</span>
cipher <span style="color:#e28964">=</span> power_mod(m,e,n)
puts <span style="color:#65b042">"Alice encrypts the message to: <span style="color:#daefa3">#{cipher}</span>"</span>

puts <span style="color:#65b042">"<span style="color:#ddf2a4">\n</span>Alice then sends her ciphered message back to Bob."</span>
</pre>

**Finally, Bob receives the ciphered message and decrypts the password by using power mod again, cipher^d mod N**

<pre >decipher <span style="color:#e28964">=</span>  power_mod(cipher,d,n)

<span style="color:#e28964">if</span> m <span style="color:#e28964">==</span> decipher
  puts <span style="color:#65b042">"Bob decrypts the message and revealed: <span style="color:#daefa3">#{decipher}</span>"</span>
<span style="color:#e28964">else</span>
  puts <span style="color:#65b042">"Unable to reveal the secret"</span>
<span style="color:#e28964">end</span>
</pre>

**No matter how many times you run the simulation, Bob will always get the same message that Alice wants to send!**

<pre>
This is an RSA Example
Random P: 432751903
Random Q: 821428381
N = 355474695055959043
PHI: 355474693801778760
The chosen E: 314375684447020309
D = 207822147779699149


Bob sends N and E to Alice.
Alice wants to send thsi message to Bob: 12345678
Alice uses E and N to encrypt the message.
Alice encrypts the message to: 74798231699119844

Alice then sends her ciphered message back to Bob.
Bob decrypts the message and revealed: 12345678
</pre>

Have a nice day,
-irevived1

