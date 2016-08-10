---
layout: post
title:  "Ruby Operator Overload"
date:   2016-08-10 21:31:00 +0000
---

08.10.2016

Operator Overload

Operator Overload, I have been overloading operators with objects before I was introduced to the term itself.  In fact, operator overload is pretty common in the world of programming languages.  We just take things for granted.  In fact, we take things for granted all the time anyways.  

Let’s define what is operator overload.  According to Techopedia, **Operator overloading is a technique by which operators used in a programming language are implemented in user-defined types with customized logic that is based on the types of arguments passed.** 

*What does that mean?*

Well, I don’t quite understand completely either, but let’s do some live coding, shall we?

Let’s take a look at the String class in Ruby.  When you define, or create two strings, you can do math on it.  Simple add them together and you can easily concatenate the two strings.  This allows you to effortlessly join the two together:

<pre >[<span style="color:#3387cc">1</span>] pry(main)<span style="color:#e28964">></span> string1 <span style="color:#e28964">=</span> <span style="color:#65b042">"Hello"</span>
=> <span style="color:#65b042">"Hello"</span>
[<span style="color:#3387cc">2</span>] pry(main)<span style="color:#e28964">></span> string2 <span style="color:#e28964">=</span> <span style="color:#65b042">"World"</span>
=> <span style="color:#65b042">"World"</span>
[<span style="color:#3387cc">3</span>] pry(main)<span style="color:#e28964">></span> string1 <span style="color:#e28964">+</span> <span style="color:#65b042">" "</span> <span style="color:#e28964">+</span> string2
=> <span style="color:#65b042">"Hello World"</span>

</pre>

**If addition works in string, let’s play with subtraction too!**



<pre >[<span style="color:#3387cc">1</span>] pry(main)<span style="color:#e28964">></span> string1 <span style="color:#e28964">=</span> <span style="color:#65b042">"Hello World"</span>
=> <span style="color:#65b042">"Hello World"</span>
[<span style="color:#3387cc">2</span>] pry(main)<span style="color:#e28964">></span> string2 <span style="color:#e28964">=</span> <span style="color:#65b042">"World"</span>
=> <span style="color:#65b042">"World"</span>
[<span style="color:#3387cc">3</span>] pry(main)<span style="color:#e28964">></span> string1 <span style="color:#e28964">-</span> string2
<span style="color:#3e87e3">NoMethodError</span>: undefined method <span style="color:#65b042">`-' for "Hello World":String
</span></pre>


Oh no, NoMethodError!  I wonder why . . 

It is because in the String library, the creator did not include the - (subtraction) operator.  Therefore, the computer does not know the logic behind it, or the meaning behind that particular operator.  Though it may seems very logical to the human brain, it is not to the computer.  The user or the creator has to manually define all operator operations for each and every object.  The best way to understand it is to treat the operator as the name of the method.  Let’s take a look at the code below:

<pre >[<span style="color:#3387cc">1</span>] pry(main)<span style="color:#e28964">></span> <span style="color:#e28964">class</span> <span style="color:#3e87e3">String</span>
[<span style="color:#3387cc">1</span>] pry(main)<span style="color:#e28964">*</span>   <span style="color:#e28964">def</span> <span style="color:#89bdff">subtract</span>(<span style="color:#3e87e3">string</span>)
[<span style="color:#3387cc">1</span>] pry(main)<span style="color:#e28964">*</span>     <span style="color:#3e87e3">self</span>.gsub(string,<span style="color:#65b042">""</span>)
[<span style="color:#3387cc">1</span>] pry(main)<span style="color:#e28964">*</span>   <span style="color:#e28964">end</span>
[<span style="color:#3387cc">1</span>] pry(main)<span style="color:#e28964">*</span> <span style="color:#e28964">end</span>
=> <span style="color:#3387cc">:subtract</span>
[<span style="color:#3387cc">2</span>] pry(main)<span style="color:#e28964">></span> string1 <span style="color:#e28964">=</span> <span style="color:#65b042">"Helloooooo"</span>
=> <span style="color:#65b042">"Helloooooo"</span>
[<span style="color:#3387cc">3</span>] pry(main)<span style="color:#e28964">></span> string2 <span style="color:#e28964">=</span> <span style="color:#65b042">"ooooo"</span>
=> <span style="color:#65b042">"ooooo"</span>
[<span style="color:#3387cc">4</span>] pry(main)<span style="color:#e28964">></span> string1.subtract(string2)
=> <span style="color:#65b042">"Hello"</span>
</pre>

**This seems so boring.  Let’s make things look more interesting with the help of operator overload.**

<pre >[<span style="color:#3387cc">1</span>] pry(main)<span style="color:#e28964">></span> <span style="color:#e28964">class</span> <span style="color:#3e87e3">String</span>
[<span style="color:#3387cc">1</span>] pry(main)<span style="color:#e28964">*</span>   <span style="color:#e28964">def</span> <span style="color:#89bdff">-</span>(<span style="color:#3e87e3">string</span>)
[<span style="color:#3387cc">1</span>] pry(main)<span style="color:#e28964">*</span>     <span style="color:#3e87e3">self</span>.gsub(string,<span style="color:#65b042">""</span>)
[<span style="color:#3387cc">1</span>] pry(main)<span style="color:#e28964">*</span>   <span style="color:#e28964">end</span>
[<span style="color:#3387cc">1</span>] pry(main)<span style="color:#e28964">*</span> <span style="color:#e28964">end</span>
=> <span style="color:#3387cc">:-</span>
[<span style="color:#3387cc">2</span>] pry(main)<span style="color:#e28964">></span> string1 <span style="color:#e28964">=</span> <span style="color:#65b042">"Hell no"</span>
=> <span style="color:#65b042">"Hell no"</span>
[<span style="color:#3387cc">3</span>] pry(main)<span style="color:#e28964">></span> string2 <span style="color:#e28964">=</span> <span style="color:#65b042">" n"</span>
=> <span style="color:#65b042">" n"</span>
[<span style="color:#3387cc">4</span>] pry(main)<span style="color:#e28964">></span> string1 <span style="color:#e28964">-</span> string2
=> <span style="color:#65b042">"Hello"</span>

</pre>

**How cool is that?**

You may also override the existing methods as well. Which means….
You can use this technique to mess with your friends !

<pre >[<span style="color:#3387cc">1</span>] pry(main)<span style="color:#e28964">></span> <span style="color:#e28964">class</span> <span style="color:#3e87e3">Fixnum</span>
[<span style="color:#3387cc">1</span>] pry(main)<span style="color:#e28964">*</span>   <span style="color:#e28964">def</span> <span style="color:#89bdff">*</span> (<span style="color:#3e87e3">num</span>)
[<span style="color:#3387cc">1</span>] pry(main)<span style="color:#e28964">*</span>     <span style="color:#3e87e3">self</span> <span style="color:#e28964">-</span> num
[<span style="color:#3387cc">1</span>] pry(main)<span style="color:#e28964">*</span>   <span style="color:#e28964">end</span>
[<span style="color:#3387cc">1</span>] pry(main)<span style="color:#e28964">*</span> <span style="color:#e28964">end</span>
=> <span style="color:#3387cc">:*</span>
[<span style="color:#3387cc">2</span>] pry(main)<span style="color:#e28964">></span> <span style="color:#3387cc">10</span> <span style="color:#e28964">*</span> <span style="color:#3387cc">5</span>
=> <span style="color:#3387cc">5</span>
</pre>


Messing with your friends is not the main purpose of this blog.  The important thing is to get the practicality of operator overload into practice.  Here is a little demo with doing subtraction and addition with an object called Circle using its area.

<pre ><span style="color:#e28964">class</span> <span style="text-decoration:underline">Circle</span>
  <span style="color:#3e87e3">@@pi</span> <span style="color:#e28964">=</span> <span style="color:#9b859d">Math</span>::<span style="color:#3e87e3">PI</span>
  <span style="color:#e28964">attr_reader</span> <span style="color:#3387cc">:area</span>, <span style="color:#3387cc">:radius</span> 

  <span style="color:#e28964">def</span> <span style="color:#89bdff">initialize</span>(<span style="color:#3e87e3"> <span style="color:#3387cc">area:</span> <span style="color:#3387cc">nil</span> , <span style="color:#3387cc">radius:</span> <span style="color:#3387cc">nil</span></span>)
    <span style="color:#e28964">if</span> area <span style="color:#e28964">&amp;&amp;</span> area <span style="color:#e28964">></span> <span style="color:#3387cc">0</span>
      <span style="color:#3e87e3">@area</span> <span style="color:#e28964">=</span> area
      <span style="color:#3e87e3">@radius</span> <span style="color:#e28964">=</span> (<span style="color:#9b859d">Math</span>.sqrt(area<span style="color:#e28964">/</span><span style="color:#3e87e3">@@pi</span>))
    <span style="color:#e28964">elsif</span> radius <span style="color:#e28964">&amp;&amp;</span> radius <span style="color:#e28964">></span> <span style="color:#3387cc">0</span>
      <span style="color:#3e87e3">@radius</span> <span style="color:#e28964">=</span> radius
      <span style="color:#3e87e3">@area</span> <span style="color:#e28964">=</span> <span style="color:#3e87e3">@@pi</span> <span style="color:#e28964">*</span> (radius<span style="color:#e28964">**</span><span style="color:#3387cc">2</span>)
    <span style="color:#e28964">else</span>
      <span style="color:#3e87e3">@area</span> <span style="color:#e28964">=</span> <span style="color:#3e87e3">@@pi</span>
      <span style="color:#3e87e3">@radius</span> <span style="color:#e28964">=</span> <span style="color:#3387cc">1</span>
    <span style="color:#e28964">end</span>
  <span style="color:#e28964">end</span>

<span style="color:#aeaeae;font-style:italic">  # Operator Overload here:</span>

  <span style="color:#e28964">def</span> <span style="color:#89bdff">+</span>(<span style="color:#3e87e3">circle</span>)
    <span style="color:#9b859d">Circle</span>.<span style="color:#e28964">new</span>(<span style="color:#3387cc">area:</span> (area<span style="color:#e28964">+</span>circle.area))
  <span style="color:#e28964">end</span>

  <span style="color:#e28964">def</span> <span style="color:#89bdff">-</span>(<span style="color:#3e87e3">circle</span>)
    <span style="color:#9b859d">Circle</span>.<span style="color:#e28964">new</span>(<span style="color:#3387cc">area:</span> (area<span style="color:#e28964">-</span>circle.area))
  <span style="color:#e28964">end</span>

  <span style="color:#e28964">def</span> <span style="color:#89bdff">*</span>(<span style="color:#3e87e3">circle</span>)
    <span style="color:#9b859d">Circle</span>.<span style="color:#e28964">new</span>(<span style="color:#3387cc">area:</span> (area<span style="color:#e28964">*</span>circle.area))
  <span style="color:#e28964">end</span>

<span style="color:#aeaeae;font-style:italic">  # having too much fun here, playing with meaningless circle definitions</span>

  <span style="color:#e28964">def</span> <span style="color:#89bdff">%</span>(<span style="color:#3e87e3">circle</span>)
    <span style="color:#9b859d">Circle</span>.<span style="color:#e28964">new</span>(<span style="color:#3387cc">area:</span> (area<span style="color:#e28964">%</span>circle.area))
  <span style="color:#e28964">end</span>

  <span style="color:#e28964">def</span> <span style="color:#89bdff">/</span>(<span style="color:#3e87e3">circle</span>)
    <span style="color:#9b859d">Circle</span>.<span style="color:#e28964">new</span>(<span style="color:#3387cc">area:</span> (area<span style="color:#e28964">/</span>circle.area))
  <span style="color:#e28964">end</span>

  <span style="color:#e28964">def</span> <span style="color:#89bdff">**</span>(<span style="color:#3e87e3">circle</span>)
    <span style="color:#9b859d">Circle</span>.<span style="color:#e28964">new</span>(<span style="color:#3387cc">area:</span> (area<span style="color:#e28964">**</span>circle.area))
  <span style="color:#e28964">end</span>

<span style="color:#aeaeae;font-style:italic">#this method overrides the puts statement</span>
  <span style="color:#e28964">def</span> <span style="color:#89bdff">to_s</span>
    puts <span style="color:#65b042">"Area:<span style="color:#ddf2a4">\t</span><span style="color:#daefa3">#{<span style="color:#8a9a95">@area</span>}</span>"</span>
    puts <span style="color:#65b042">"Radius:<span style="color:#ddf2a4">\t</span><span style="color:#daefa3">#{<span style="color:#8a9a95">@radius</span>}</span>"</span>
  <span style="color:#e28964">end</span>
<span style="color:#e28964">end</span>

a <span style="color:#e28964">=</span> <span style="color:#9b859d">Circle</span>.<span style="color:#e28964">new</span>(<span style="color:#3387cc">radius:</span> <span style="color:#3387cc">2</span>)
b <span style="color:#e28964">=</span> <span style="color:#9b859d">Circle</span>.<span style="color:#e28964">new</span>
puts a <span style="color:#e28964">*</span> b

<span style="color:#aeaeae;font-style:italic">#output</span>
<span style="color:#3e87e3">Area</span>:   <span style="color:#3387cc">39.47841760435743</span>
<span style="color:#3e87e3">Radius</span>: <span style="color:#3387cc">3.5449077018110318</span>
</pre>

Ta da!

I hope you have enjoyed it and have a nice day,

-irevived

