# REACT_ES6_ES2016_Tutorial

This is a repository containing the notes from the following tutorial I followed on LinkedIn learning : https://www.linkedin.com/learning/react-es6-es2016-and-beyond . 

# Variables and Declarations

**const, let and var**

There are three types of variables in javascript : var, const, let. The differences are shown below.

<img src="https://github.com/aiday-mar/Images/blob/master/Variable_Types_JS.JPG"/>

We can output the value of the variable say `a=2` without specifying the var keyword in front, this is an example of hoisting. However this will throw an error saying that the variable is used before it is defined. Suppose now that you were to use the `const` keyword in front instead, then this would not be possible, because `const` can not be reassigned before it is declared. The following is not possible :

```
a = 2
const a = 3
```

However the above is possible with the `let` keyword meaning that you are able to write for example :

```
b = 2
let b = 3
```

Furthermore const variables are read-only but not immutable. The fact that const variables are not immutable implies for example that it is possible to create a const array and then push some new entries into that array. It is possible to freeze a const rray so that it is no longer possible to push entries to it. This can be done by writing the following code :

```
Object.freeze({const variable})
```
We can consider an example of how the `const` and the `let` keywords can be used in conjunction, for example when declaring a link to an API : 

```
const ApiLink = {link}

let options = {
  method : "POST",
  headers : {
    "Content-Type": "application/json"
  },
  body : JSON.stringiy({})
}
```
In order to be able to use a class in another file we need to use the keywords `export` in fron of a class definition. When you specify `default` in front then this means that when you export a class from that file, then this class will be exported by default. One thing to note is that you can not have this `export default const`, however you can specify a `const` class and then `export default` it in another line. On the same page you can export a couple of classes by writing as so : 

```
export {class1, class2..}
```

You can also use aliases as so :

```
import {OneClass} as {AnotherClass}
```

**CSS Styles**

Now we want to use the ``styled-components`` library in order to add some styles to our page. We can do this for all our classes for example by writing as so:

```
import styles from `styled-components`

export const Container = styled.div
  display : flex;
  flex-direction: row;
  margin: auto;
  justify-content: space-around;
```

Now for example in a javascript class file you can write the below : 

```
import React, { Component } from `react`
import { Container } from `./styled`

class App extends Component {
  render() {
    return (
      <Container>
      .
      .
      .
      </Container>
    )
  }
}
```

**arrow functions**

Arrow functions allow us to simplify code, in the following for example we have two functions which fundamentally do the same thing :

```
withACallBack('so long', function(options) {
    return options
  }
}

withACallBack('very short', options => options)
```

The arrow functions though are different to the traditional functions though. Consider the following code :

```
export function arrowFunctions() {
  
  adress : '5th Avenue'
  
  const store = {
    address : '101 Main Street'
    what: function() {
      return this.address
    }
    arrow : () => {
      return this.address
    }
  }
}
```

The `this` keyword in the what function consider the scope of the store object. The `this` keyword of the arrow function considers the scope of the arrowFunctions class and therefore will output ``5th avenue``.

We can apply the knowledge above to our options objects from the beginning and in fact change this object into an arrow function as follows :

```
const ApiLink = {link}

let options = () => {
  method : "POST",
  headers : {
    "Content-Type": "application/json"
  },
  body : JSON.stringiy({})
}
```
Now we study destructuing. This is a simplified way of accessing object attributes as follows : 

```
const feast = {
  appetizer : 'spring rolls',
  entree : 'enchiladas',
  dessert : 'apple pie',
  beverages : {
    wine : 'merlot',
    water : 'sparkling',
  }
}

let {
  appetizer
  dessert
} = feast

console.log('appetizer=', appetizer)
console.log('dessert=', dessert)
```

Instead of writing `console.log('feast=', feast.appetizer)` . This method allows us to access deeply nested variables. We can also access the variables in the following way :

```
let {entree, beverages: {wine}} = feast
let {water} = feast.beverages
```
We can access a deeply nested variable and furthermore rename it using the following syntax :

```
let {dessert:favorite} = feast
```

You can also destructure by using an array with no key-value pairs but just values by using the following code :

```
const horsdoeuvre = ['crab cakes', 'spring rolls', 'fried pickles', 'caviar']
let [crabCake,,,grossFishEggs] = horsdoeuvre
console.log(crabCake)  // "crab cake"
console.log(grossFishEggs)  // "caviar"
```
We use the above in an `OnChange` example as follows :

```
class App extends Component {
  
  // but if we want to later reassign a state variable called editor then we need to 
  // initially inialize it with some empty string for example
  
  state = {
    editor: ""
  }
  
  handleChange = (event) => {
    let {name, value} = event.target
    this.setState({
      [name] : value   
      //meaning now we access the value in the editor by accessing the name of the editor, 
      // and you can apply this handleChange function not only to the editor but to other components as well
    })
  }
  
  render(
    let {value} = this.state
    let {handleChange} = this
    .
    .
    .
    <Editor
      name="editor"
      value={value}
      onChange={handleChange}

  )
}
```

In the above the name is always editor but the value changes depending on what is written inside the text area.

# Arguments and Template Literals

**spread operator**

The spread operator allows you to pull appart the parts of an array and make use of them as though they were instead a series or collection of values, rather than a traditional array. You can join array as follows :

```
const sauces = ['bbq', 'buffaloe', 'honey mustard']
const dressgings = ['ranch', 'balsamic']
const superSecretSauce = [...sauces, ...dressings]
```
You can also apply the same logic to classes as follows :

```
const favoriteToppings = {
  peanutButter : 'crunch'
  jelly : 'strawberry'
}

const sandwhich = {
  breadSlices : 2,
  ... favoriteToppings
}
```

You can also achieve the above effect by writing :

```
const sameSandwich = Object.assign({breadSlices : 2}, favoriteToppings)

```

The above command essentially takes two objects and combines them into one. In a similar fashion you can pass all the props to a container by writing :

```
<{component name} {...props}>
```
**template literals**

You can initialize a string and pass some variables inside, as follows :

```
let exclamation = 'woaw'
let noun = 'jumbo jet'

const madlibs = `"Oh ${exclamation}"! they said. "I've never seen a ${noun} before!"`
```
We apply the previous knowledge to a button displayed on the previous HTML page in order to create a new field. We do this as follows :

```
rules = () => {
  let {rules} = this.state  // object destructuring will tell us how many rules we have
  let array = []
  let fields = ['name', 'begin', 'end']
  for (let i=0; i < rules; i++){
    array.push(
      <Row key={i}> // the i is then the index of the row
        <Column>
          {fields.map((field, index) => {
            return() {
              <Column key={index}>
                <RuleLabel>
                  {field}
                </RuleLabel>
                <RuleInput 
                value={this.state[`${field}${i}`]]
                onChange={this.handleChange} 
                name={`${field}${i}`}
                />
              </Column>
            }
          })}
        </Column>
        <StyleInput 
          value={this.state[`style${i}`]}
          onChange={this.handleChange}
          name=(`style${i}`)
        />
      </Row>
    )
  }
  
  return array
}

newFields() => {
  this.setState( (prevState) => {
    let {rules} = prevState
    lets fields = ['name', 'begin', 'end', 'style']
    let inputValues = {}
    fields.forEach( (field) => {
      inputValues = {
      ...inputValues,
      [`${field}${rules}`]:''
      }
    })
    rules++
    return{
      rules,
      ...inputValues
    }
  })
}

render() {
  let {newFields, rules} = this
  .
  .
  .
  {rules()} // here then rules will return an array of components
  <Button onClick={newFields}>
}
```

You can use the three dots in the arguments of a function too as follows :

```
function F(...args){
  console.log(args)
}
```
# Classes

When you declare a class, then you can also declare a constructor that goes with it, and that has two parameters in it. The constructor gets called when you instantiate the object. When you extend a class and you write the constructor you need to write in the constructor the keyword super to signify that we are calling the constructor of the parent class. In other words 

```
class ColorGenerator extends Random {
  constructor({arguments of super class}, {additional arguments}){
    super({arguments of super class})
  }
}
```
You can also have getters and setters for the functions as follows :

```
get types() {
  return this.typeList
}

set types(types=['hex', 'rgb']){
  if (Array.isArray(types)) {
    this.typeList = types.map(type => type)
  }
}
```

# Promises and Async

**promises**

The promises allow us to make asynchronous actions in javascript. Promises are often included in functions. The syntax is as follows :

```
return new Promise((resolve, reject) => {})
```

In the above resolve and reject are themselves functions that are invoked inside the promise. Resolve is invoked when the promise has done what it had to done. Reject is invoked when something in the promise has gone wrong. Consider the example below :

```
function waitUpToThreeSeconds(seconds) {
  return new Promise ((resolve, reject) => {
    
    setTimeout(
    () => {
      reject('3 seconds are up ! You asked me to wait for too long!')
    },
    3000
    )
    
    setTimeout(
    () => {
      resolve('${seconds} seconds are finished!')
    }, 
    seconds*1000
    )
  }
}
```
In the above we are racing reject and resolve against each other. You can invoke the functions as such :

```
waitUpToThreeSeconds(2)
  .then(successMessage => {console.log(successMessage)})
  .catch(errorMessage => {console.log(errorMessage)})
```
When the resolve method is envoked the .then is envoked.
When the reject method is envoked the .catch is envoked.

**fetch**

You can make promise enabled HTTP request without using an outside library by using the following syntax :

```
fetch(urls, options).then(resp => {...})
```
An example is written below :

```
// response.text() and response.buffer() also avilable
fetch(shakespeareApi, options()).then(response => response.json()).then(
  // this is what we have to run on the promise returned by response.json()
  json => {console.log(json)}
)

const shakespeareApi = "https:// ..."

let options = () => {
  return{
    method : "POST",  // this can be get, post, delete
    headers : {
      "Content-Type" : "application/json"  // the headers attached to the request
    },
    body : JSON.stringify({
      query : `{
        allPoems(
          first : 1
          skip : ${rando.randomInt(0, 160)}
        ) {
          title
          author
          lines
          text
        }
      }`
    })
  }
}
```

**async and try/catch**
