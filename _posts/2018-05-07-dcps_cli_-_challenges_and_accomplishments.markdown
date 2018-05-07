---
layout: post
title:      "DCPS CLI - Challenges and Accomplishments"
date:       2018-05-07 14:27:11 +0000
permalink:  dcps_cli_-_challenges_and_accomplishments
---


I created a scraper to pull information about schools and principals from the DCPS website and allow users to search them through the command line.  Below I have outlined some of the things I found especially challenging (but I pulled them off!) and things I would do differently.


### Interesting challenges:

* **Searching by Grade**: I wanted to allow users to search for schools by grade level.  This was tricky because the schools on the website have a grade range with their lowest and highest grades (e.g. PK3 - 8th or 9th - 12th) but not a list of every grade they teach.  To convert this into something searchable, when schools are instantiated they  convert their grade range into an array of all the grades they contain. The oldest and youngest grades aren't simple numbers like 5th or 8th, so I converted "PK3", PK4", "kindergarten", and "adult" into numerical values so I could then create an array for each school with the range of grades between the lowest (e.g. -2 if a school had PK3) and the highest (up to 13 if a school serves adults).  When a user wants to search by grade, it either converts the necessary word into the numerical value or pulls the number from whatever they've entered (e.g. "5th" instead of "5") and searches the grade array for each school and returns all schools that contain that value.  


* **Searching by Last Name**: When I conceptualized this program searching by principal last name seemed like an easy and obvious feature but it was harder than I'd assumed because the principal names are not broken out into component parts on the website.  Some principals have titles or middle names included so I couldn't just split up the names at spaces.  To get around this, the first and last names actually come from principal email addresses.  The email addreses are structured "firstname.lastname@dc.gov" so getting last names out of those was pretty easy and the user has no way to view just the first or last name attributes of a principal so the formatting doesn't have to be pretty.  I did make myself absolutely crazy trying to figure out why this wasn't working when I realized that some principals' email addresses were firstname.lastname and some were Firstname.Lastname; making all of them lowercase solved this problem.  There is at least one principal with a hyphenated last name who looks like she pops up in a weird spot in the alphabetical order because her email address is only the second half of her name but that makes it seem like she's comfortable with that as a last name so I'm okay with it too.

* **Controller Options**: I wanted users to be able to view details on a school or principal and execute searches without returning to the main menu every time.  This meant that I needed to keep track of whatever search results they'd most recently viewed and be ready to display them again.  I also wanted to allow users the option of either trying a new search or returning to the menu if their search didn't turn up any results. I am hopeful that the code looks simple enough not to reflect my  frustration with this because it meant fiddling with a number of methods to make sure they were all based on the same assumptions about how the controller would work, e.g. making sure that I didn't have a method that displayed "No search results found" which called another method that also displayed "No search results found".  This also involved a lot of recursion to deal with invalid inputs but I find recursion very satisfying so that part was fine.

### What I Would Do Differently Next Time

Oh man there is so much I could say here which is proof this was a good learning experience.  Here are some initial thoughts:

* I really should have mapped out everything I wanted to do more carefully before I started.  I was nervous and excited and also just wanted to get the scraper DONE so I sort of plunged in without mapping everything out.  That would have saved me a lot of frustration later.

* I wish I had included clearer descriptions of the methods initially, especially the arguments they take.  I built the scraper and then built everything else while using test values and then when it was time to put the whole thing together I spent like twenty minute staring at the scraper methods trying to figure out what order they were supposed to go in to scrape the site properly to return an array of hashes to instantiate the objects.  I'm sure this is really obvious to people with more experience than I have but if I had included clear information/notes for myself when I started I would have been a lot happier.

* Next time I will think more carefully about what I expect to do a lot of times, including prompts for users.  For example, if I just had a method that put "That is not a valid entry." I wouldn't have had to search through my code to make sure I phrased that the same way every time.  If I started with simple methods for that kind of output from the beginning I would have been able to change it in one place if I wanted it to say something different.

For all that there are things I would do differently (and if I were to do the same thing a year from now I'm sure it would look much more elegant) I feel pretty proud of this project!  I haven't put something like this together entirely by myself before and it felt good pulling live information from a website instead of something set up for educational purposes.  I was especially proud of my search methods, particularly the grade level searches.  Of course if you have any questions, please don't hesitate to contact me.  Thank you for taking the time to read this and for your interest in my project!



