---
layout: post
title:      "Command Line Interface - Published GEM"
date:       2017-11-08 10:37:41 +0000
permalink:  command_line_interface_-_published_gem
---

Reading through instructions for the CLI Gem project, it felt a bit overwhelming. The toughest part was figuring out where to begin. When doing labs, we have the benefit of rspec test suite, which after running, will tell us what is failing. This gives me a starting point of what I can tackle first. One skill that I came to realize is necessary in development, is the ability to compartmentalize the entire project into small junks. First, I imagined what I wanted my application to do. Without worrying about the implementation details, I just envisioned what the end user would experience. This helped me get an idea of the general process of what the application will do and thus I could focus in on the entry points of the application. Sometimes it becomes hard to NOT think about the whole picture all at once, but trusting in yourself and the process, were just a few contributing factors that drove me to successful completion of this project. 

I decided to create a Gem that scrapes the Cinemark website for all their upcoming movies. I wanted to display the movies to a user in a list and allow them to select one to see all the details available for that movie.

There were times during the process, where I questioned my website choice for scraping. At the time I did not have the adequate knowledge to tackle the problem at hand. I found it relatively easy to figure out the initial selector to scrape all the movies and the seemingly only thing left to do was to figure out how to retrieve all the individual movie details. This is where I hit a roadblock. I came to realize that I will have difficulties achieving my goal, since A) not all the movies displayed the same amount of details, and B) there was nothing unique about each element listing the detail in the DOM. 

The full list details for a movie consisted of: Release Dates, Rating, Runtime, Genre, Cast, Director, Synopsis and Official Site. Some movies had all the details listed, while others only displayed four and, yet others displayed details with empty values. An example would be "Rating" without any data listed. 

When debugging a movie website in Nokogiri I successfully figured out the CSS selectors to find all the details for the first movie I was working with. The problem was that since the HTML details elements were not uniquely identified, my CSS selectors relied on indexes of certain elements. This issue quickly surfaced when scraping a movie that had less details listed. For instance my CSS selectors always expected “Cast” to be in the 4th index position. Here is an example of how the HTML elements looked like:
```
<div class="hidden-xs">
                        <h3>Release Dates</h3>
                        <p> December 14, 2017


                        </p><h3>Rating</h3>
                        <p></p>

                            <h3>Runtime</h3>
                            <p>150 min</p>
                    </div>						
```
The main div where all details are listed has a class called “hidden-xs”. Thinking about how I could solve this problem, I came across a new idea for selecting items. Instead of using a CSS selector, I could use Xpath and tell Nokogiri to find HTML elements that contained certain strings. At this point I could tell Xpath to check if the main div has an ‘h3’ element with the string ‘Genre’ in it, if it did I just grabbed the sibling element inner text. 

Xpath came in handy for my situation and turned out be more flexible than CSS selectors. Xpath has a bit different syntax than CSS and allows for more complex selectors.
This was a challenging project but one that felt very rewarding at the end. The biggest pay off was publishing the Gem and asking a friend to install it on their machine. They could run the Gem with two lines of code and run it as a complete package. I enjoy scraping websites and using that information to drive the application. 






