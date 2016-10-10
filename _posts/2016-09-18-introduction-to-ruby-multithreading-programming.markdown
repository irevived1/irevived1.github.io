---
layout: post
title:  "Introduction to Ruby Multithreading Programming"
date:   2016-09-18 10:00:00 -0400
---


09.18.2016

Introduction to Ruby Multithreading Programming

Let’s say you are attending an art class and you need to produce two assignments.  One of them needs to apply glue to it and the other is just plain drawing.  In order to complete the task in the shortest amount of time, a little scheduling is required to perform the task.  Normally you wouldn’t  apply the glue and wait for it to dry, you would apply the glue and then move on to the drawing assignment while waiting for the glue to dry.  Congratulations, you just multithreaded yourself, if that’s even proper English.

The concept about is essentially what your operating system is doing all the time.  Not for each little program, but for all the applications that are running in the background and in the foreground.   The CPU is so fast that it performs this task for a moment and moves on to the next task for a brief amount of time.  It creates the illusion that the computer is doing everything at once.  If you zoom in the time frame, you can actually see the CPU is grinding on task A while all other tasks are in a frozen state.  Then it moves to task B and all other tasks will be frozen.  When you zoom out the time frame, humans aren’t fast enough to realize your CPU is playing tricks on you.  (This scenario is describing single core CPUs, multi-core cpus does not apply)

Going back to multithreading, the OS treats a single process as multiple processes.  However, we don’t call them processes anymore, we call them threads.  Or, if you like, you may call it a lightweight process.  To visualize how it actually works, take a look at the diagram below:

![Diagram1](https://www.tutorialspoint.com/operating_system/images/thread_processes.jpg)

This image was optained from [https://www.tutorialspoint.com/operating_system/os_multi_threading.htm](https://www.tutorialspoint.com/operating_system/os_multi_threading.htm)

In a multithreaded program, every thread has its own register, counter and the stack pointer, which pretty much acts like individual processes but the data and files are being shared.  Whereas a single threaded program is just sharing everything inside and out.

Enough with the theory, let’s look at some basic code.

For Windows, it is important to define your function with the return type of DWORD

and include the library ``#include<windows.h>`` and if you are using Linux you’ll have to include ``#include <pthread.h>``.

Just kidding, Ruby programmers don’t need to worry about these.  

```ruby
def function
  #do your magic here
end


#initialize your thread and pass your function here
thread1=Thread.new{function()}
#put .join or the main thread will end the execution.
# .join tells the main thread to wait for the little thread to finish, then it gives permission to end it
thread1.join

```

Simple enough right? Let’s do some performance tests on a threaded program and non-threaded program.  Consider the following:

```ruby
require 'time'

t1 = Time.now
$num = 0;
$tmp = 0

def function1
  while $num < 1000000000
    $num +=1
    if $tmp != $num/50000000
      puts "Hello from fucntion1! #.#{$tmp+1}"
      $tmp = $num/50000000
    end
  end
end
function1
t2 = Time.now
puts "Total: took #{t2-t1} seconds."

```

The program above increments the variable **num** to a billion and stops the execution.  In the meanwhile, it also says hello every 50 million.
It takes about a minute to finish running on an i5 macbook.
And now, multithreaded version!  We have three functions to increment the same counter **num** to a billion.  

```ruby
require 'time'

t1 = Time.now
$num = 0;
$tmp = 0

def function3
  while $num < 1000000000
    $num +=1
    if $tmp != $num/50000000
      puts "Hello from fucntion3! #.#{$tmp+1}"
      $tmp = $num/50000000
    end
  end
end

def function2
  while $num < 1000000000
    $num +=1
    if $tmp != $num/50000000
      puts "Hello from fucntion2! #.#{$tmp+1}"
      $tmp = $num/50000000
    end
  end
end

def function1
  while $num < 1000000000
    $num +=1
    if $tmp != $num/50000000
      puts "Hello from fucntion1! #.#{$tmp+1}"
      $tmp = $num/50000000
    end
  end
end

thread1=Thread.new{function1()}
thread2=Thread.new{function2()}
thread3=Thread.new{function3()}
thread1.join
thread2.join
thread3.join
t2 = Time.now
puts "Total: took #{t2-t1} seconds."

```

Though, I cannot see your face, but I can tell you are quite disappointed.  The program above took longer than the single threaded program.  This is very disappointing.

Going back to the art class analogy,  the computer threats all input and output operations like glue.  It is slow because humans are slow, keyboard is slow, mouse is slow, your monitor is slow.  It is nothing compared to the speed of the CPU.  IO is the burden of the process.  Now, if we can put the output on one of the functions and leave the other two to do the increment, maybe we will see a different result.  Maybe.

```ruby
require 'time'

t1 = Time.now
$num = 0;
$tmp = 0
def function3
  while $num < 1000000000
    $num +=1
  end
end

def function2
  while $num < 1000000000
    if $tmp != $num/50000000
      puts "Hello from fucntion1! #.#{$tmp+1}"
      $tmp = $num/50000000
    end
  end
end

def function1
  while $num < 1000000000
    $num +=1
  end
end

thread1=Thread.new{function1()}
thread2=Thread.new{function2()}
thread3=Thread.new{function3()}
thread1.join
thread2.join
thread3.join
t2 = Time.now
puts "Total: took #{t2-t1} seconds."

```

Ah ha!  Now we are talking.  It almost doubles the execution time, though we have used three functions.  But hey, the performance has increased.

Conclusion:

It is very important when it comes to writing a multithreaded program.  It is crucial to know where and when to put the inputs and outputs in the appropriate place.  Once you have it down, multithreading program will definitely speed up your performance as you can see.  Another thing you’ll have to watch out for is the having multiple functions to access the same variable.  For more information, please visit: [Tutorials Point](http://www.tutorialspoint.com/ruby/ruby_multithreading.htm)

Have a nice day,

-irevived1
