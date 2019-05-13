---
layout: post
title:      "Ionic React todo list"
date:       2019-05-13 16:09:16 +0000
permalink:  ionic_react_todo_list
---


Today we will be exploring the Ionic framework. Ionic is a great tool for developing cross platform apps(web, iOS, android). Ionic is traditionally used with angular however ionic/react is in beta and should be released soon. To start off cd into an appropriate folder to hold your project and enter. 

````
$ create-react-app ionic-todo --typescript
$ cd ionic-todo
$ npm install @ionic/react react-router react-router-dom @types/react-router @types/react-router-dom
$ atom .

````

Now locate the App.tsx file src/App.tsx and rename the file to App.js and besure to change the import statement inside index.tsx to App.js also. 

Go back to App.js and add the following import statements 

````
import '@ionic/core/css/core.css';
import '@ionic/core/css/ionic.bundle.css';
import {
  IonApp,
  IonContent,
  IonCard,
  IonCardHeader,
  IonCardTitle,
  IonItem,
  IonList,
  IonLabel,
  IonInput,
  IonButton
} from '@ionic/react';

````

Next add the constructor method. 

````
constructor(){
    super()
    this.state = {
      todos: [],
      newTodo: ""
    }
  }

````

Here we are setting the components initial state to have an empty array of todos and an empty string to hold the new todo. 

Now add these helper methods inside the app component

````
  addTodo = () => {
    this.setState({todos: [...this.state.todos, this.state.newTodo], newTodo: ""})
  }

  todoChanged = (event) => {
    this.setState({newTodo: event.target.value})
  }

  removeTodo = index => {
    let arr = this.state.todos.filter((todo,i) => i !== index)
    console.log(arr)
    this.setState({todos: arr})
  }

  renderToDoList = () => {
    return this.state.todos.map( (todo, index) => {
        return (
          <IonItem>
            <IonLabel>{todo}</IonLabel>
            <IonButton onClick={() => this.removeTodo(index)}>Remove</IonButton>
          </IonItem>
        )
      })
  }


````
These methods will interact with the state to update accordingly when a todo is added or removed. rederToDoList will iterate over our list of todos and render an Ionic component for each one. 

Finally we need a render method

````
render() {
    return (
      <IonApp>
        <IonContent>
          <IonCard>
            <IonCardHeader>
              <IonCardTitle>Your Todo List</IonCardTitle>
            </IonCardHeader>
          </IonCard>

          <IonItem>
            <IonInput placeholder="Enter ToDo..." onIonChange={this.todoChanged} value={this.state.newTodo}>
            </IonInput>
            <IonButton fill="outline" onClick={this.addTodo}>Add Todo</IonButton>
          </IonItem>

          <IonList>
            {this.renderToDoList()}
          </IonList>
        </IonContent>
        <IonContent>

        </IonContent>
      </IonApp>
    );
  }

````

Now in the terminal enter npm run start and you should see your todo list using ionic working. 
Here is the finished [project.](https://github.com/harryFBloch/ionic-todo)
