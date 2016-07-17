---
layout: post
title:  "Ruby Command Line Argument"
date:   2016-07-17 15:52:48 -0400
---

07.17.2016

Ruby Command Line Argument

We have all used command line arguments one way or the other if have ever properly used the terminal.  In fact, bash commands are filled with commands with arguments.  For example:

	cd ../to/some/path
 
*in this case, ‘../to/some/path' is the argument for the cd command*

	cp file1.txt file2.txt
 
*file1 is the first argument and fil2 is the second argument*


Even a simple command like ‘ls’ can take arguments as well.

	ls -la

*-la stands for Lists All files,including the hidden files*

We take nice things for granted all the time.  Imagine the world without command line arguments so we can realize its importance.  Without arguments, all the commands we use in bash has to be user interactive, meaning, it will ask for user to prompt in inputs every time.  

	~$ cd
	~$ Where would you like to go? ../to/some/path
	~../to/some/path$
	
This is actually not that bad, try the *mv* command to move files around

	~$ mv
	~$ Which file do you want to move?  ../some/path/file.txt
	~$ Choose your destination: ./file1.txt

It would be really annoyed if you have made a typo at “*Choose your destination:*” because then you will have to go through it again from the beginning.  

The easiest way to understand command line argument is to treat the command itself like a function or a method.  If you have ever written or programmed before, it is basically the same idea. 

	def some_method( arg1 , arg2 )
	   #some code here
	end


The only difference I can think of is that a method or a function has a limited number of arguments which the user can define.  Whereas the command line arguments has no limitations.  Although the program may accept an array of arguments, the programmer can set a limit to the program.  In other words, the command line argument is simply an array of **string** that the user inputs whenever they run the program.

Most of the programming language such as Java, Python, Perl, and even Ruby, the first argument will be will be saved in the array with the index of 0.  However, there are exceptions. Programming language such as C/C++ will save the name of the program as the first argument by default.  It means when you use the array of arguments in C/C++, array index of 0 will return the name of the program.  

### Using Command Line Arguments in Ruby:

A simple way to obtain the array of arguments in Ruby is to simply use the default constant ARGV, this array may be empty if the user did not provide any.  Another way to access the argument array is ARGF.argv.  (*ARGF is a whole different topic which contains extra functionalities such as STDIN and more*) Please keep in mind that the type of the array is an array of **String** by default.  You may convert it to integer or float if mathematical computation is required.  

### Let’s see a live code example in Ruby:

	#sums up all the integers

	#user input validation omitted
 
	if ARGV.empty?
		sum = 0
		input = ""
		loop do
			print "Enter your number or 'exit' to quit: "
			input = gets.strip
			break if input == "exit"
			sum += input.to_i
		end
		puts "Sum is: " + sum.to_s
	else
		puts "Sum is: " + ARGV.inject(0){|total,x| total+=(x.to_i)}.to_s
	end


The program first checks if the ARGV array is empty by using the #empty? method.  You may also use the other array method from the Array class.  If the array is empty, then it goes into the section with user interaction:

![user interactive](https://raw.githubusercontent.com/irevived1/img-dump/master/tty-1.gif)

	sum = 0
	input = ""
	loop do
		print "Enter your number or 'exit' to quit: "
		input = gets.strip
		break if input == "exit"
		sum += input.to_i
	end
	puts "Sum is: " + sum.to_s

It takes this many lines to perform a program with user interactive functions.
Whereas a program with command line arguments, it only takes this one line to get the job done:

	puts "Sum is: " + ARGV.inject(0){|total,x| total+=(x.to_i)}.to_s
 *User input validation omitted*

![commandline](https://raw.githubusercontent.com/irevived1/img-dump/master/tty-2.gif)

Awesome right?  Use ARGV when you can!  Let’s all live inside the terminal.

-revived1


##### source: http://ruby-doc.org/core-1.9.3/ARGF.html#method-i-argv

