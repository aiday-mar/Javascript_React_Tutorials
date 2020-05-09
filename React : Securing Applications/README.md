# React : Securing Applications 

In this Read Me file I wrote the notes taken during the LinkedIn course "React : Securing Applications". As an example you can write :

```
npm install flow-bin
npm run flow init
npm run flow 
```
The latter command runs the flow. Then we also need to install ESlint.

```
npm install -g eslint
npm info
```
The corresponding files should have an `.eslintrc` extension. 

The OWASP project also named : Open Web Application Security Project. It contains references to potential attacks on the internet. Cross-site scripting (XSS) attacks, is when a malicious script is injected into a trusted site. Some example of attacks have been pulling data from cookies, session tokens, and all kinds of sensitive information. If you try to directly set the property `innerHTML`, this is not permitted according to the error, and instead one should use `dangerouslySetInnerHTML`. But this leaves our code vulnerable to attacks.

Cross-Site Request Forgery is malicious code that can be injected when a user is authenticated to a trusted web site. To prevent CSRF we have two methods. Either : first check the header to validate the request, the request URL needs to be from the same HTTP URL as the server. You want to avoid CORs or Cross-Origin Requests. After this we check for encrypted or signed token, which should be provided with the request. If both checks are approved then the transaction can be completed. We implement this security with Auth0 which is a popular call-based authetication service. Auth0 also add preventive measures against threats such as cross-site scripting.

Let's now study JSON Web Token or JWT, this is an open standard that is used to securely transmit information between parties. A JSON object consists of a header, the payload, the signature. The header has two parts, the type of token and the hashing algorithm used. The payload consists of metadata, of data such as (issuer of request, expiration,name). Auth0 uses also the JWT services. The payload can be used to transmit information from any two parties.

The backend needs to be built with some API inputs. Next to the `src` folder you can create two folders : `server` and `client` folder. All the elements in the project will be put into the client folder and our securing fode goes into the server folder. You can create a package.json file in the project directory as follows by typing `npm init`, followed by 

```
npm install --save body-parser cors body-express express-jwt jwks-rsa nodemon
```

The above are the main dependencies that will be used. Then we also need to install the dev dependencies : 

```
npm install --save-dev babel-cli babel-preset-env babel-preset-stage-0
```

In the package.json file we write the following :

```
"scripts" : {
  "test" : "echo test"
  "start" : "nodemon ./index.js --exec babel-node -e js"
}
```

In our `index.js` file we write :

```
import express from 'express';
import jwt from 'express-jwt';
import cors from 'cors';
import jwks from 'jwks-rsa';
import bodyParser from 'body-parser';

const app = express();

app.use(bodyParser.json());
app.use(bodyParser.urlencode({extended : true}))
app.use(cors());
app.get('/courses', (req,res) => {
  let courses = [ {data goes in here} ],
  res.json(courses);
})
app.listen(4000, () => {consolelog('Server is running on port 4000')});
```

In the `.babelrc` file we write :

```
{
  "presets" : [
    "env",
    "stage-0",
  ]
}
```

In the course we installed Postman from www.getpostman.com and opened the application. Inside the GET search bar you can type : `localhost:4000/courses` this will be the API endpoint. Then you can click on `send` and that way get the data from the server.
