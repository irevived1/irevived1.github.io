---
layout: post
title:  "First Collaboration"
date:   2016-07-28 12:51:18 +0000
---


07.27.2016

Flatiron Sinatra Assessment

I have been doing all my labs alone during my time in the fellowship program.  I am very inexperienced of pairing up with somebody or working together with someone for small scale projects.  My instructor has easily spotted my noticeable lonely behavior.  So she paired me up with somebody who also has been doing all her assignments alone.  I thought it would be a challenge for the both of us until i realized everything has already worked out fine.  

In this assessment, we had to build an MVC (models,views,controllers) Sinatra Application.  Each model has to use ActiveRecord with Sinatra and there has to be multiple models.  The models needed to be in complex relationship using *belongs_to* and *has_many* keywords.  Users must be able to login and logout.  This includes user creation and account modification as well.  Password validation will also be included in this project.  Though this assessment may sound like a lot of sweat, but it was actually not that bad and it was rather enjoyable to do.  

My partner, **thecarsgone**, spent some time on Monday afternoon to talk about which topic we will be doing.  We have talked about and made agreements on division of labor.  It did not take us long to come up with a topic because she already has the initial idea.  Our website will be a website which allows the user to create a user, login logout, uploads pictures and modify the picture ratios.  I will be mainly handling setting up the structure of the program and dealing with the User model.  While my partner will be dealing with picture editing and the Picture model of the project. 

My portion of the project was pretty straight forward.  I structured the program like the previous labs we did in Learn.co.  Put the gem called *shotgun* so I can get real time results if I changed the layout or the content of the website.  I have used rake db:migrate_create to create both the Users database and the Pictures database.  The *users* database is consist of only the user name and a password digest.  The *pictures* data base has the name and the user id.  **thecarsgone** requested to insert a column called *ratio* for pictures.  So I have added an extra migration to add the column.  Finally, the migration is completed and it is time to set up the models.  The user has many pictures and the picture belongs to a user.  Everything looks good and I proceeded to edit the Application section.  There weren’t any trouble maker glitches in the code and the whole process was rather pleasant.  Upon user creation, the program will create a directory for that particular user so the user will be able to store multiple pictures in his or her personal directory.  The website has a welcome page to lure people to login or sign up.  After signup, the user will be redirected to the login page.  Upon login, the *login* and *signup* button will disappear and will merge into a button called *logout*.  The user index page consist of all the pictures the user have been uploaded.  

**thecarsgone** handles most of the heavy duty picture manipulations such as providing the option to upload pictures in different ratio aspects.  If the user wanted to have custom ratios, there you go, custom ratios are also available in the picture creation webpage.  After uploading the picture, the user will have the option to modify the ratio or remove the picture completely.  The database and the files will automatically re-adjust to match the user’s action.

### Challenges

The coding part of the lab was and bad.  We never thought that using github was the most challenging task in this collaboration.  We were inexperienced with github and I was panicking when I saw the conflict error message while merging the pull requests.  I have also made a breakthrough in terms of number of commits.  In the past, i have only made a few commits because I was working alone and I did not see the necessity to commit often.  However, working in a group will kind of force you to commit often.

### Benefits

Doing projects with somebody will definitely reduce the workload dramatically.  I know I am stating the obvious.  The real benefit is you can learn by reading your collaborators code.  If you don't understand something, just ask.  Having some type of human interaction is great too, it can relieve boredom at times.  
Working in a team is as just as important as your coding skills. 

### Special thanks to:

 - **thecarsgone**
 - My instructor, **Ruchi**

-irevied1 

