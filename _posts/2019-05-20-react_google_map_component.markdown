---
layout: post
title:      "React Google Map Component"
date:       2019-05-20 16:59:54 +0000
permalink:  react_google_map_component
---


Today we will be taking a look at how to use a library called react-google-maps. We will be building a simple reusable component to leverage this library. To get started cd to an appropriate folder for your project in the terminal and run. 

````
$create-react-app react-map
$cd react-map 
$atom .
````
While your machine is creating the app run over to https://developers.google.com/maps/documentation/javascript/get-api-key and get an api key

Now let's set up the dependencies run 
````
$npm i react-google-maps
````

Next create a new file called src/MapComponent.js and open it up. 

First lets add the import statements on top 

````
import React, {Component} from 'react'
import { withGoogleMap, GoogleMap } from 'react-google-maps'
````

Next We will create the component

````

export default class MapComponent extends Component {

   render() {
   const GoogleMapExample = withGoogleMap(props => (
      <GoogleMap
        defaultCenter = { { lat: this.props.lat, lng: this.props.lng } }
        defaultZoom = { 13 }
      >
      </GoogleMap>
   ));
   return(
      <div>
        <GoogleMapExample
          containerElement={ <div style={{ height: `500px`, width: '500px' }} /> }
          mapElement={ <div style={{ height: `100%` }} /> }
        />
      </div>
   );
   }
}
```` 

Here we are initializing a GoogleMap with our desired preferences and lat and longitude that will be passed in as props from the parent component. 

Next open up app.js and import the MapComponent we just created
And add this to the render method. 

````
<MapComponent lat={40.756795} lng={-73.954298}/>
````
Note: you can set the lat and lng to whatever coordinates you would like
Now there is one final step we need to tell googlemaps what our api key is and you should always keep yours hidden but for this project we will add 

````
<script src="https://maps.googleapis.com/maps/api/js?key=YourAPIKeyHere"></script>
````
Add this at the end of your <head> tag inside index.html 
Run npm start and you should see your map!

