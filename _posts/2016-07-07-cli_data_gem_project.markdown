---
layout: post
title:  "CLI Data Gem Project"
date:   2016-07-07 14:16:02 +0000
---


07.06.2016

Weather

I have finally reached the final project assessment as the third week approached me during my time in Flatiron School.  There were example domains of topics where students can choose.  Searching for nearby libraries, nearby Restaurants or movies, etc.  I felt like these domains are probably too popular and it would be redundant for me to create another one.  I couldn’t come up with a topic so I walked around for a few minutes, realized that it was raining and I thought it would be great to have a little weather forecast in my terminal.  Today is the birth of my little weather gem.  
	I thought programming was hard, who would have thought searching for the right website for my Nokogiri to work would be harder.  I have searched through dozens of website on google and none of them satisfies me.  Most of them requires users to enter a location or it is not fetchable like the google weather.  It was a lot of sweat and pain just to look for the right site for my project.  
Finally I have decided to settle for Yahoo News Weather.  It is a clean interface with 10 days of forecast right out of the page.  Forgot to mention, it's got a really nice background image as well.  I have used Nokogiri to test if the content was fetchable, after a while I was able to get the data that I needed for this project.  It was tricky because there were clearfix classes being used and Chrome was not able to show visual highlight for the blocks that I needed.  With a bit of determination it was no longer a problem.
My incapability has limited me from designing a complex structure, so the only choice i have left was to create a simple program.  I can only come up with three classes and they are:

Scraper: A scraping class that only handles Nokogiri for gathering data from the website
Day: This day class stores the weather information for each day.
Weather: This weather class performs string manipulation and strips the data and save each one of them into the Day class.

Let's take a look at each one of them in detail.  

The Scraper class does not need to be initialized.  It only has two methods.  Just call its function by doing Scraper.scrape_page(*Your_URL_Here*) and you are good to go.  This method returns a string which can be further processed by Nokogiri.  The next method called *Scraper.otherdays* which processes the returned value of *#scrape_page* and returns an array of string which holds the 7 days of forecast including today.  The Scraper class was also provided DIY Error messages to handle exceptions when misused.  

The Day class is rather simple because it only holds and prints its data values.  It has four attribute macros, __day__*(stores which day of the week)*, __high__*(stores the higher temperature of the day)*, __low__*(you know this one already)*, __status__*(describes the status in 2 words)*, __info__*(long descriptive information includes Celsius as well)*.  This class only contains two methods, the *#print method* prints all the information including the detailed descriptive of that particular day.  The *#printlite* function is a mini-version of the *#print* function with only the day of the week, temperature and its status.  

The Weather class is the heavy duty class.  It has an array of Day class with 7 elements.  Additional Day variables named today and tomorrow acts as pointers to point to the current day and the next day respectively.  This is crucial because the program needs to know which day to start iterating.  Without it, the program will just iterate from Monday every time.  During the initialization of the class, the class fetches information directly from yahoo.com/news/weather and begin its job.  It calls *Scraper.scrape_page* and *Scraper.otherdays* for string manipulation.  Within the initialization, it also parse the string and stores the day, high, low, status, and info for each and every Day variable.  Additional method called *#refresh* refreshes the status if needed.  A bunch of print methods are also implemented for ease of use.  Please see the usage below:

 ### __USEAGE__

This program defaults to two-day forecast if no argument is provided.

To use the available arguments, please look at the flags below.

* -t Prints the weather for tomorrow.
* -n Prints the weather for today.
* -w Prints the weather for the whole week.
* -d Add this flag behind the others for detail information. eg: -td , -nd, -wd..
* -h --help for help"
* ISSUE? visit https://www.yahoo.com/news/weather and enable your geolocation.

WARNING: This application may not work if Yahoo changes its web news interface.

Enjoy the little program and have a nice day,
https://github.com/irevived1/weather-cli-gem

-irevived1

