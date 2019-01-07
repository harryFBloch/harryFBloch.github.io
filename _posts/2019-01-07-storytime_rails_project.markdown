---
layout: post
title:      "Storytime Rails Project"
date:       2019-01-07 15:00:53 +0000
permalink:  storytime_rails_project
---


For my third project for the flatiron school online web developer bootcamp. I chose to create a web app called storytime. Storytime allows users to sign up using their google account or creating a new account with email and password. Users can then upload a photo to start a new story or contribute to another story that is already started. The only catch is that you can only add one sentence at a time. After that the user needs to wait for someone else to post a sentence before they will be able to again. It will be very interesting to see what kind of stories people can come up with as a community. 

The two biggest challenges I ran into for this app where learning to user paperclip in order to store images in a database, and learning to use the google oauth strategy. With paperclip it was very important to validate that a user uploaded a file and that the file was in fact an image this was accomplished using these three validators

````
 has_attached_file :image
 validates_attachment_presence :image
 validates_attachment_content_type :image, :content_type => /image/
````


