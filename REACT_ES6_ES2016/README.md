# REACT_ES6_ES2016_Tutorial

This is a repository containing the notes from the following tutorial I followed on LinkedIn learning : https://www.linkedin.com/learning/react-es6-es2016-and-beyond . There are three types of variables in javascript : var, const, let. The differences are shown below.

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
