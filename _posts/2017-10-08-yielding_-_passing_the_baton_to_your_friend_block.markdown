---
layout: post
title:      "Yielding - "passing the baton" to your friend "block""
date:       2017-10-08 13:33:18 +0000
permalink:  yielding_-_passing_the_baton_to_your_friend_block
---


Learning new coding concepts can be difficult. Especially if you don't have reference points from your life experiences to relate to topic you're trying to understand. Making progress through the course, I found it difficult to fully understand the behavior of the "yield" keyword. Therefore, I decided to write about it and explain how it works. Walking through and explaining newly acquired topics can be a good way to test yourself on the new material and learn.

Some of the questions I am hoping to answer in this blog are:
1. What are blocks and where do they belong?
2. How does the *yield* keyword work, and what is its relationship to the block?

So Block - what is it? googling....and then I had my "Aha!" moment 

Block is simply the code between `do` and `end` keywords

Blocks come in two versions:
1. Multi-line `do` and `end` - Typically used when the logic inside the block needs more than one line
2. Inline `{` and `}` - Typically used when you have simple logic that fits on one line

*There is slight behavior difference between `{}` and using `do` and `end` keywords. Curly braces take precedence over using the keywords, this article touches on this point:* [http://rubylearning.com/satishtalim/ruby_blocks.html]

Example of a block:

`["cat", "dog", "mouse"].each { |n| puts "This is #{n}"}` - example of an inline block.

In the above example the block is the entire code between the curly braces. I think it might help to know that blocks are their own functionality can supplement method calls in performing certain action(s). This can help us manipulate the outcome and flow of our program.

Example of block used on a method:

Let's say we have a method called `names_starting_with_o(list)` that takes an array as a parameter, which in our case will be an array of first names. Assuming our method has logic that will iterate over every name in the list and return each name at a time that begins with the letter "O'. Knowing this we can call a block on our method.

`names_starting_with_o(list) do |o| puts "Welcome #{o}" end`

Now we can say that: *`names_starting_with_o(list)` method **yields** each name starting with "O" to the block".*
We say it yields each name to the block, because once it finds the first name that starts with "O" it will step out of the method and give that parameter to the block. In which case it will return back to the method and continue executing following the same pattern.

Lets look at the implementation of our method to fully understand how it works:

```
def names_starting_with_o(list)
    list.each do | o | #The block variable "o" represents each name in the list
      if ( o.start_with?("O")) #If condition is true we enter the code block
        yield (o) #At this point in our code, we have the variable
     end           #Starting with the letter "O" 
   end             #Now we will take it, and return to the method block.
 end
```
 
Yield keyword in this scenario passes one parameter to the block. Yield keyword can pass zero or more parameters to the block. 







