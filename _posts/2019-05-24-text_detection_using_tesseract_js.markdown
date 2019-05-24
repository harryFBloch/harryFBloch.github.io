---
layout: post
title:      "Text Detection using Tesseract.js"
date:       2019-05-24 16:41:27 +0000
permalink:  text_detection_using_tesseract_js
---

In this blog post i will be going over using Tesseract.js for text detection in images. First think you need to do is install the tesseract.js module with npm. Navigate to your projects directory and enter.

````
$ npm install tesseract.js@next --save
````

Next in your app.js or wherever you plan to use text detection add the following code 

````
import React, {Component} from 'react';
import {IonLabel} from '@ionic/react'
import { TesseractWorker } from 'tesseract.js';
import myImage from './bedfordave.jpg'
const worker = new TesseractWorker();

export default class App extends Component {

  constructor(){
    super()
    this.state = {
      imageText: ""
    }
  }

  componentDidMount(){
    worker.recognize(myImage)
    .progress( p => console.log('progress', p))
    .then( result => {
      console.log(result)
      this.setState({imageText: result.text})
    })

  }

  render(){
    return (
          <p>{this.state.imageText}</p>
    )
  }
}
````

First we initialize a tesseract worker and then supply it the image in the componentDidMount life cycle method. Then we simply are storing the resulting text to the components state and rending it onto the screen. Checkout to the result object for lots of cool data like words and accuracy of the text that was detected. 

