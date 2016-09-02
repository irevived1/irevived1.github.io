---
layout: post
title:  "Flatiron Rails Assessment"
date:   2016-09-01 21:19:30 -0400
---


09.01.2016

Flatiron Rails Assessment

It’s been a while since I did my previous assessment.  The reason why is because there are so many lessons in the Rails section, 104 lessons!  Though it was a long section, but I did not rush through them.  I took my time and worked my way through all the lessons.  Just like every other sections for Flatiron School, there will be an assessment waiting for you at the very end.

Coming up with a topic is always the most difficult task for these assessments.  The possibilities are endless.  However, there are some restricted domains such as ToDo lists, Blog Posts, and Amusement Parks.  I am glad that they made restrictions so it will help me narrowing down my choices.  Finally, I have decided to make a website that allows user to add notes to their home page.  Each note will be connected to a subject and a user.  With table relations, it will be handy to sort through the data and get only the notes that belongs to the user and belongs to that particular subject.

Generating Rails’ structure is just as easy as generating resources.  Rails spoils people so much, with a few commands on the CLI and there you have it.  It really didn’t take long to have a running rails server with nothing in it.  Howevers, this is where the hard part kicks in.  

Implementing Devise and OmniAuth for Facebook login can be tricky.  I had to follow the documentation really carefully.  A simple typo can be devastating.  At this stage of the project, it is just about copying and pasting the right code from the documentation and putting them in the correct files.  Shortly after, the website is on and users will be able to sign in, sign up and sign out through Devise.  

Nested forms and routes is really time consuming.  It took me a good amount of time to implement all the working functionalities as desired.  The labs in Rails have prepared me well for this assessment because I have done it a handful of times.  Without the restriction of Rspec, making nested application is even easier.  This section of the project is rather enjoyable and it is one of the painless process to go through.

**Challenges**

I find it challenging to implement bootstrap, and CSS styling in my project.  I have never added any styling for my previous Rail labs.  I had to do my own research and start adding CSS myself.  I came across Twitter-Bootstrap-Rails from [https://github.com/seyhunak/twitter-bootstrap-rails](http://) and it saved my life.  It’s got really nice documentations.  It comes in the form of a gem and all I had to do was include the list of gem names they provided, ran bundle install and there we go.  The rest is just generating with rails generator.  All the CSS and embedded ruby files come with predefined CSS classes and ids.  The hard part was I had to redo all my erb files.  I did not know by generating the stylings will overwrite my current erb files.  I had to make a copy and then generate the file, and manually change everything on my own.  It look me an hour and a half to change everything.  It was worth it though, not my website looks all nice and pretty.  I also learned it the hard way that I should always pick a theme for CSS first because I do the logic part of the project.

**Problems**

There was this weird problem that I have encountered when I was dealing with *datalist* for html in this project.  A *datalist* gives all the available options in the form of the combination of a dropdown menu plus a flexible form.  My datalist will display all the previously *subjects* that have been created.  The users may select one of the option or create their own options.  It all worked fine except that the datalist was unable to show the last option from the database.  It displayed every options except for the very last column from the database.  The name of the last column was replaced by raw SQL output which is weird:

Math
Biology
Geography
< id: 1, name: “math”, …. > , < id: 2, name: “biology”, …. > , < id: 3, name: “math”, …………….>

Obviously there was something wrong with something.  I was unable to pinpoint the exact problem.  So I modified the code and changed some stuff around.  As I was at the verge of giving up, I decided to manually iterate through all the subjects.  I set a variable with an array of all the subjects, made a boundary of the length of all the subjects and an iterator to iterate through all the subjects and display it on the datalist.  For some odd reason, doing it manually worked.  The last line of SQL data is no longer displaying.  The datalist is now displaying properly.  However, it is not an elegant solution because it is not recommended to put a too much logic in the views.  This odd problem still remains a mystery, there aren’t anything related problems that i could find on Google.

**Conclusion**

Overall, I had fun doing this assessment.  I feel like assessments are great for self-learning compared to labs.  Labs are well structured in a way which is hard for me to see the overall concept.  Students will most likely to tackle specs by specs which loses bigger picture.  Assessments are great when it comes to uniting all the things we have learned and putting it together, which compensates the flaws of the labs.  I have learnt valuable lessons such as generating layouts before coding the functionalities.  It would definitely save me a lot of time in the future.

-irevived1
