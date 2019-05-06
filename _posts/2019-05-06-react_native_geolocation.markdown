---
layout: post
title:      "React Native GeoLocation"
date:       2019-05-06 16:41:56 +0000
permalink:  react_native_geolocation
---


Today we are going to take a look at the Geolocation API for React-Native. The geolocation api exists on the global navigator object in React Native, just like on the web, so you would access it via navigator.geolocation.

First things first we need to get permission from the user to access location. For iOS this is enabled by default but just incase you need to set NSLocationWhenInUseUsageDescription to True in the info.plist. However this is usually defaulted to true. But for andriod the user is prompted when downloading the app instead of on first use, so you need to add 

````
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />

````
To your AndroidManifest.xml

Now it is time for the fun part actually calling the methods on navigator. Add the following inside the componentDidMount. 

````
navigator.geolocation.getCurrentPosition(
      (position) => {
        console.log(position)
      },
      (error) => this.setState({ error: error.message }),
      { enableHighAccuracy: true, timeout: 20000, maximumAge: 1000 },
    );

````

If you run the above code you should see the position object printed to the console. Now you can call position.coords.latitude or position.coords.longitude, or just pass the whole position object to a reducer and add the location coordinates to the redux state. 

There are a few other methods to consider depending on the use case for you app. getCurrentPosition returns the position of the user once. watchPosition will get called again every time the users position has changed. Finally clearWatch this should be used every time watchPosition is called to tell your app to stop tracking location. 

