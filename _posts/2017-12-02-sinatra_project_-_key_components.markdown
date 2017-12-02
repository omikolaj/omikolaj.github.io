---
layout: post
title:      "Sinatra Project - Key Components"
date:       2017-12-02 15:01:30 +0000
permalink:  sinatra_project_-_key_components
---

Learning Sinatra and *ActiveRecord* has been the most insightful and fun learning experience thus far. My first impressions were that Sinatra was really built for the developer and aimed to make their task of building dynamic web sites fast and easy. I found that as a developer, reading and understanding error messages expedites the troubleshooting process, giving you more time to focus on coding. The more functionality the application has, the more complex the implementation becomes. Sinatra makes a great leap in helping us understand where an error occurred with very descriptive error messages that point us directly to the core of the problem. That leaves few key components that we need to keep in mind when putting all of the puzzle pieces together to make the entire application feel well structured, designed and secured.

**Structure:**

The structure of web application should be easy enough so that other developers can look at the implementation and understand how the puzzle pieces link together. We want to keep the scaffolding of the Sinatra application, follow a common pattern and structure. Using `gem install corneal` achieves just that. It will build out the structure of our application for us, following the common patterns.

Database schemas. When starting my projects, the first thing I look at is how my models will be relating to each other. It helps me see the bigger picture of what I want to accomplish. It often helps to draw these relationships out, especially when working with `has_many` to `has_many` relationships that require a *JOIN table* to represent that relationship. Even though rolling back the database migration is not difficult task with *ActiveRecord::Migrations*, we can simply call `rake db:rollback` and drop the database tables, allowing us to modify any migrations we might have missed. Not fully understanding the relationships can become problematic when troubleshooting issues later in the process.

**Design:**

To prevent running into errors when building out the application, it might be a good idea to mount all of our controllers in the *config.ru* file that our application will need to access. We can only specify one `run ApplicationController`, and the rest of the controllers need to be mounted with prefix with `use`.  When our server receives requests, we have access to all of our controllers and their routes.

*Views*. The web application we work on can grow to be a large application with many different views. Grouping the views in files that correspond with each controller makes it easier to follow and maintain. Stubbing them out before we start coding will give us a good visual representation of what views our controllers' routes will render. This will also decouple the views from each other, following a best practice pattern, separation of concerns. 

**Security:**

Security is one of the most important aspects of building and designing a web site. Especially one working with a database that stores user's private and personal information. Using `gem 'bcrypt'` will help us keep our users passwords secure. *'bcrypt'* has to be included in our Gemfile. Once it is installed, the model that will represent the user, needs to have *(Inherit from ActiveRecord::Base)* `has_secure_password` keyword. This mechanism will add few very important validations for our application. One of which is that it will require that the password is present when presisting it to the database. `has_secure_password` also adds additional  methods, one of which is called `authenticate` that we use to validate the user that is logging in, is using the same password that is stored in the database. Next, the database migration that creates our user's table, needs to have a column specifically called "`:password_digest`". Even though we are creating a column called "`:password_digest`", we can refer to it by calling "`password`"  on an instance of the user class . We can't forget that our view that will render the form for either signing a user up or to log them in, must have an `<input type="password">` field on it in order to properly obfuscate it. Otherwise, any string entered in the password field on our form will be visible.

To further help keep our website secure, we need to make sure that we are always checking that the current user that is surfing our web sites pages, is someone that is logged in. We should not allow just anyone to that visits our website view, modify or even delete content they have not authored. I found the use of helper methods to be very beneficial in making this an easy process. The helper methods should be defined in the main ApplicationControl. These helper methods will set the `current_user` to the user that is logged in, and when called, check for us if the user that is visiting one of our routes is in fact the user that is logged in.

These are just some of the key components that I keep in mind when building out my Sinatra applications. Understanding the fundamentals of how Sinatra works "under the hood" so to speak, allows me to leverage  that knowledge to feel confident in reading Sinatra documentation and implement new features. After all, all we are doing is adding additional methods to our classes and expanding our functionality.  







