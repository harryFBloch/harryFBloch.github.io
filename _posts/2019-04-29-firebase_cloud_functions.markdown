---
layout: post
title:      "Firebase Cloud Functions"
date:       2019-04-29 15:56:53 +0000
permalink:  firebase_cloud_functions
---


In this blog post I will be talking about firebase cloud functions. Firebase cloud functions are used when you want to perform some action on your firebase data on the back end. We will go over a simple way to filter the data return by a user ID. 

If you do not already have the firebase CLI installed in the terminal run 

```` npm install -g firebase-tools ````

Create a project in the firebase console go to the functions tab and click get started.

Then click continue twice and go over to the database tab and click on get started in test mode.
Make sure on the top next to where it says Database that “Real time database” is selected no cloud firestore.

Now lets add some dummy data to the database to play around with I added 

```` users: {1: {name: Harry}, 2: {name: bob} ````

Next go back to the terminal and cd to an appropiate location for the project and make a new folder for it.

````mkdir firebase-cloud-functions-test````

Then
````cd firebase-cloud-functions-test````
````firebase init````


Select functions and press “space” then enter.

Select your project name from the list you want to link it with.(if you don't select a project when you run firebase deploy add “---project your-project-name”)

Next select “JavaScript”, Yes for eslint, and yes for install dependencies.

Once complete open the folder in your text editor of choice.
````atom .````

Go to functions/index.js 

Go to your firebase console select project settings and navigate to the service accounts tab.
Click Generate new key

Create a new file in Your functions folder called serviceAccountKey.json and paste your newly generated key into that file. I would suggest adding this file to your gitignore because anyone with access to that key will have access to your firebase account. 

Open up index.js and add

````
const admin = require('firebase-admin')

var serviceAccount = require("./serviceAccountKey.json");

admin.initializeApp({
  credential: admin.credential.cert(serviceAccount),
  databaseURL: "https://cloud-function-test-8d77f.firebaseio.com"
});

//make a request with userID and return that User
exports.returnUser = functions.https.onRequest((request, response) => {
 const id = request.body.id
 const ref = admin.database().ref('users/' + id)
  ref.on('value', snapshot => {
    //no need to continue listening for value changes
    ref.off()
    response.send(snapshot.val())
  })
});

````

Here we are retrieving the user by their id and returning a snapshot of the user with json.
Open up Postman if you do not have it already download it here https://www.getpostman.com/downloads/.

Make a post request to your function URL you can find it under the functions tab on firebase or in the terminal logs once firebase deploy was complete. 

Now select body and set it raw and JSON (application/json) and enter in the body 
````
{
	“Id”: 1
}

````
Click send and your response should be. 

````
{
	“name”: “Harry”
}
````

You have successfully completed your first firebase cloud function that even gets access to the database. 

