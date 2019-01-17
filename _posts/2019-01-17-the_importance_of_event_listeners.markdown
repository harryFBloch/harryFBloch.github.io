---
layout: post
title:      "The Importance Of Event Listeners"
date:       2019-01-17 14:41:02 +0000
permalink:  the_importance_of_event_listeners
---


The importance of using event listeners in java script cannot be stressed enough. Event listeners are responsible for all the fun things we can do on a webpage. For example click, keydown, keyup, mouseover, mouseout.... Without event listeners users would not be able to interact with websites and they would be pretty boring. Thankfully javaScript makes it easy for use to add event listeners to objects in the DOM. Open up the developer console on this page and enter.

````
title = document.querySelector('h1')
title.addEventListener("click", event => {alert("You Clicked the Title")})
````

Now if you click on the title of the article you should see an alert pop up that says “You Clicked the Title”.

