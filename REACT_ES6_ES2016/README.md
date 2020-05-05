# REACT_ES6_ES2016_Tutorial

This is a repository containing the notes from the following tutorial I followed on LinkedIn learning : https://www.linkedin.com/learning/react-es6-es2016-and-beyond . 

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
