---
layout: post
title:      "Goalie-Tracker React/Redux Final Project"
date:       2019-03-06 20:40:29 -0500
permalink:  goalie-tracker_react_redux_final_project
---


For my final project at Flatiron school I was tasked with using all of my knowledge learned in the course to create a single page web app. The technologies that used to create this app where a Rails backend and a React/Redux front end. I created a hockey goalie tracking app where you can enter statistics while your watching a hockey game. There are four main routes in the app one to create a new game, one to enter data on the current game, list all stats for goalies, and list all games. 

The biggest challenges I faced while creating this app where figuring out how to turn a picture into a bunch of buttons and how to chain async actions using redux. I overcame these challenges by reading stack overflow and creative thinking. 

My first challenge was to turn this picture into a bunch of different buttons. If you click on one of goalies pads it records a save on that pad, or if you click on one of the numbers a goal is recorded for that hole. 

![](http://dearsportsfan.com/wp-content/uploads/2015/02/Goalie-Holes-1.png)

I achieved this by creating an array of all the x and y mouse coordinates for those parts of the picture. It was also important to subtract the scroll offset from the mouse position coordinates so that no matter where you called if you click that picture it will trigger the correct event. 

My other big challenge was to figure out how to chain redux actions with thunk. Our class only briefly went over thunk so this was all new to me enter stack overflow to the rescue. After some searching I learned that you can just chain them like so.  

````
export function getGames(gameId){
  return (dispatch,getState) => {
    return dispatch(getHomeGame(gameId)).then((resp) => {
      let awayGameId = resp.homeGame.oppsoing_game_id
      return dispatch(getAwayGame(awayGameId)).then(() => {
        return dispatch({type: "GAMES_LOADED"})
      })
    })
  }
}
export function getHomeGame(gameId) {
  return (dispatch) => {
    dispatch({type: 'START_GETTING_HOME_GAME'})
    return fetch(`http://localhost:3000/games/${gameId}`)
    .then(resp => resp.json())

    .then(homeGame => dispatch({type: "GET_HOME_GAME_SUCCESS", homeGame}))
  }
}

export function getAwayGame(gameId) {
  return (dispatch) => {
    dispatch({type: 'START_GETTING_AWAY_GAME'})
    return fetch(`http://localhost:3000/games/${gameId}`)
    .then(resp => resp.json())
    .then(awayGame => dispatch({type: "GET_AWAY_GAME_SUCCESS", awayGame}))
  }
}

````

Here the GetGames function is calling the getHomeGame and getAwayGame dispatch actions asynchronously. 

