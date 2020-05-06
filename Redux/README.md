# Redux 

Flux is a design pattern developed by Facebook. It is an alternative to MVC, MVP and MVVM. Changes are initiated with actions, actions are dispatched with the dispatcher, the dispatcher sends the action to the appropriate store. The store holds data, when the store updates the data, that change updates the view. When the user interacts with the view, a new action is generated and the process starts all over again. Redux is a flux implementation.

In redux the flow is from the action, to the store, to the view. There is only one store, meaning that all the states are located in one place. We create functions to manage parts of the current state. We therefore use functions to manage modularity. Redux was developed using the functional programming paradigm. It consists of three principles : pure functions, immutability (not able to change existing variables, but you can add new variables), composition (of functions).

# Understanding Reducers

First we need to install babel as follows :

```
npm install babel-cli --save-dev
```

We also install the latest and the stage-0 presets :

````
npm install babel-preset-latest --save-dev
npm install babel-preset-stage-0 --save-dev
````

This installs a babel-node command in the .bin folder. Then in the package.json file we can change the content to :

```
{
  "name": "ski-day-counter",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts":{ "start" : "./node_modules/.bin/babel-node ./src/"},
  
  "author" : "",
  "license": "ISC",
  "dependencies": {
    "babel-cli" : "^6.16.0",
    "babel-preset-latest": "^6.16.0",
    "babel-preset-stage-0": "^6.16.0",
  }
}
```

The version numbers may have to be changed depending on the babel version. 

Reducers are pure functions designed to manage specific parts of our state object. Now in our state, there is a variable called goal and now we will create a reducer for this variable in the state object.

```
import C from '../constants'

export const goal = (state=10, action) => {
  
  if (action.type === C.SET_GOAL) {
    return parseInt(action.payload)
  } else {
    return state
  }
}
```

This reducer is used below :

```
const state = 10
const action = {
  type: C.SET_GOAL
  payload: 15
}

const nextState = goal(state, action)

console.log(`
  initial goal : ${state}
  action : ${JSON.stringify(action)}
  new goal : ${nextState}
`)
```
