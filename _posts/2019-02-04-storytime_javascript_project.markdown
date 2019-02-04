---
layout: post
title:      "StoryTime JavaScript Project"
date:       2019-02-04 15:43:29 +0000
permalink:  storytime_javascript_project
---


For this months project at flatiron school I was tasked with going back over my last project Storytime that is a full rails app, and add an api to the project along with ajax calls instead of reloading the page every time a button is pressed. Storytime allows users to sign up using their google account or creating a new account with email and password. Users can then upload a photo to start a new story or contribute to another story that is already started. The only catch is that you can only add one sentence at a time. After that the user needs to wait for someone else to post a sentence before they will be able to again.

The biggest challenge for me in the project was getting posts to the api to work correctly at first i was getting an error about having no csrfToken. Finally after a while of searching on google and trying many different things i found that adding:

````
headers: {'X-CSRF-Token': Rails.csrfToken()}
````
On my post request properly passed the token along and things started to flow smoothly after that. One thing that I did to make this project super DRY and clean was create helper methods for my requests:

````
function fetchGetHelper(url,callback){
  fetch(url,{
    method: "GET",
    headers:{
      contentType: 'application/json; charset=utf-8',
    }
  }).then(resp => resp.json().then(callback))
}
````
This function is for all of my get requests it takes in a url and a callback function. 
````
function ajaxPostHelper(url, body, callback){
  $.ajax(url,{
    method: "POST",
    contentType: 'application/json; charset=utf-8',
    data: JSON.stringify(body),
    headers: {'X-CSRF-Token': Rails.csrfToken()}
  }).then(callback).fail(error => console.log(error))
}
````
This function is very similar to the last one but with two differences it makes a post request and also takes in a body variable that should be a dictionary. 
````

