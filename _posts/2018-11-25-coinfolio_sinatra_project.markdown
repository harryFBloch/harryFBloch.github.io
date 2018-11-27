---
layout: post
title:      "Coinfolio Sinatra Project"
date:       2018-11-25 11:05:31 -0500
permalink:  coinfolio_sinatra_project
---


For my second project at Flatiron school we were challenged with creating a CRUD MVC app using the sinatra gem. I decided to further extend my first project from a CLI app into a web app. I created a simple cryptocurrency portfolio tracking app. That allows users to sign up and then add coins to their portfolio so you can see what is going on with all your coins in place. 

	My biggest challenges with this project was figuring out how to pass data from ruby to javascript, learning to use materialize, and lazy loading images on the coin index page. I was able to overcome these problems with help from stackoverflow.com, the materialize documentation, and the w3schools website. 

	When passing ruby objects to javascript functions not only did you need to embed the object in erb tags <%=@object %>. It was also necessary to tell javascript what data type is being passed this can be accomplished by surrounded in quotes for a string “<%=@object %>”. 

	When lazy loading the images you provide a default image as the src and the link to your image as the data-src attribute. Then you can use javascript to figure out which images are present in the current view and update the src of only the images the user can see. 

	Another fun feature that I implemented with javascript was being able to search available coins on the index pages. This was helpful because there are 100 coins to choose from in the app and it makes an easy seamless way to find the coin you're looking for along with its current price. 

