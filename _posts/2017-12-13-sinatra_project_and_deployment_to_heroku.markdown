---
layout: post
title:      "Sinatra Project and Deployment to Heroku"
date:       2017-12-13 11:20:19 +0000
permalink:  sinatra_project_and_deployment_to_heroku
---


Finishing up last few labs leading up to the Sinatra project I wasn't sure what kind of application I would create, but I knew I wanted it to include three major pieces of technologies that I have not worked with before. They would be PostgreSQL for my database, an external API to receive data from and populate the database with and use Heroku for deployment. I often heard people use words such as "deploy" and "APIs" in reference to projects or ideas, but since I have never used them myself, it was hard to wrap your mind around what all goes into implementing them. I knew that "deploy" meant "making it production ready" and "API" was some "in code" interface that you could plug into and make calls to. Little did I know that completing this project would shine light on all those concepts in great depth and so much more.

Thanks to `gem "corneal"` I was able to quickly stub out the structure of the application but what was I going to be creating? Sometimes, this can be the toughest part of the process and I just wanted to start coding. I decided to approach the situation from the "data" perspective, so to speak. Googling "open source APIs" brought me to a GitHub page with a list of APIs to choose from. After couple minutes ... or perhaps it was hours now that I think about it, I settled on an idea. A RESTful countries API that returns details about 250 countries around the world. It was a great way to get started with an API. I found documentation to be very helpful and easy to follow. To use the API, I needed to include two extra gems in my project `gem "rest-client`" as well as ` gem "json"` which allowed me to make a call to the external source, parse the JSON file and store it in a variable. The parsed data was a hash making it easy to manipulate and work with.

PostgreSQL was the next challenge I needed to harness before moving forward. PostgreSQL uses a different approach to creating databases than SQLite3 does and just like with anything else, it is not necessarily "harder" rather different. PostgreSQL uses roles and owners that create databases. Everything here is configured at the command line level. Since the installation creates and starts a database server for you, role creation and configuration are left up to the end user. PostgreSQL has great documentation and after some time of trying different commands everything started to fall into place. With a few tweaks to my environment file I was able to successfully perform my first migration. 

Heroku was probably the biggest unknown, but it turned out to have taken the least amount of time. It's a fantastic service and that I will take advantage of in my future projects. One of the few obstacles I had to overcome during my Heroku deployment was an H10 error when trying to open my application. It had to do with favicon.ico. Reading deeper in Heroku logs, pointed out that my favicon.ico path was incorrect in my layouts, which kept returning 500 error. 

Sinatra project solidified my understanding of routes, actions and views. It was a great challenge and opportunity to put everything I have learned together. There is just something fantastic about having the ability create your idea in code and then see it come together, as one working application. It is very satisfying and rewarding which is why I love coding and the more I know the deeper the passion gets.

