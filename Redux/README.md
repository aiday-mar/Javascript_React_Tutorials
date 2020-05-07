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
We can also write the above in a more concise way :

```
export const goal = (state = 10, action) => 
  (action.type === C.SET_GOAL) ?
  parseInt(action.payload) : 
  state
```
Consider another reducer as follows :

```
export const errors = (state=[], action) => {
  
  switch(action.type){
  
    case C.ADD_ERROR :
      return [...state, action.payload] // meaning that the action.payload is added at the end of this state array
      
    case C.CLEAR_ERROR :
      return state.filter((message, i) => i !== action.payload) // when true then added to the array, when false, then filtered out of the array
      
    default :
      return state
  }
}
```
We can also compose reducers as follows :

```
export const skiDay = (state=null, action) => 
  (action.type === C.ADD_DAY) ?
  action.payload :
  state
  
export const allSkiDays = (states=[], action) => {
  
  switch(action.type) {
    
    case C.ADD_DAY :
    
      // the below command checks whether the state array has some entry that is equal to payload.date. If this is the case then hasDayAlready takes on the value true.
      const hasDayAlready = state.some[skiDay => skiDay.date === action.payload.date]
      
      return (hasDayAlready) ? state : 
      [...state, skiDay(null, action)]
    
    case C.REMOVE_DAY :
      
      return state.filter(skiDay => skiDay.date !== action.payload)
      
    default :
      return state
  }
}
```

It is possible to build challenges in order to test the reducers. This is somewhat similar to unit testing.

```
npm run challenge -a
```
We have a challenge folder under the src folder. However one challenge presents an error because the corresponding reducer is not coded. Here is the reducer :

```
export const fetching = (state=false, action) => {
  
  switch(action.type) {
  
    case C.FETCH_RESORT_NAMES :
      return true
    
    case C.CANCEL_FETCHING :
      return false
    
    default :
      return state
  }
}
```

The corresponding challenge is :

```
import C from '../constants'
import expect from 'expect'
import {fetching} from '../store/reducers'

const action = {
  type : C.FETCH_RESORT_NAMES
}

const state = false
const expectedState = true
const actualState = fetching(state, action)

// the below is like the JUnit testing
expect(actualState).toEquak(expectedState)

// if the above is true then we output that the challenge is passed
console.log(`
  Challenge A : FETCH_RESORT_NAMES Passed !
`)
```
We can now install redux as follows :

```
npm install redux --save 
```

Having installed the above library, now we can construct the below combined reducer that has to mirror the structure of the JSon file.

```
imoirt {combineReducers} from 'redux'

export default combineReducers ({

  allSkiDays,
  goals,
  errors,
  resortNames : combineReducers({
    fetching,
    suggestions,
  })
})
```

We can use this combined reducer as follows, here below the single reducer is named addReducer, it is the reducer which is by default exported from the file :

```
import C from './constants'
import appReducer from './store/reducers'
import initialState from './initialState.json'

state = appReducer(state, {
  type : C.SET_GOAL,
  payload : 2,
})

state = appReducer(state, {
  type : C.ADD_DAY,
  payload : {
    "resort" : "Mt. Shasta",
    "date" : "2016-10-28",
    "powder" : false,
    "backcountry" : true,
  }
})

state = appReducer(state, {
  type : C.CHANGE_SUGGESTIONS,
  payload : ["Mt Tallac", "Mt Hood", "Mt Shasta"],
})

console.log(`
  
  Next state
  =============
  goal : ${state.goal}
  resorts : ${JSON.stringify(state.allSkiDays)}
  fetching : ${state.resortName.fetching}
  suggestions : ${state.resortNames.suggestions}
`)
```

# The Store

