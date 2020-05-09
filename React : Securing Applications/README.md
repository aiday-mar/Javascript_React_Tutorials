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

Then you can go to www.auth0.com to sign up to the website. Scopes allow us to authorize specific endpoints for our API. When you create an API on Auth0, the website creates the client already. When you scroll down to client type you need to choose 'single page application'. In the allowed callbacks URLs we can write : 'https://localhost:3000/callback' . In the allowed origins tab write : 'https://localhost:3000'.

After some work upon the folder structure, we can open the client folder, the src folder and the auth folder. In the `auth0-variables.js` we have the following code :

```
export const AUTH_CONFIG = {
  domain : {domain name},
  clientId : {client id you find after registering}
  callbackUrl : 'http://localhost:3000/callback'
}
```

There is also an `Auth.js` file which is generated for us by the webiste when we download a sample app. There is also a `components` folder and it contains a file called `Callback.js` which contains code that will be rendered while we're connected to Auth0.

The Callback.js file is as follows :

```
import React, { Component } from 'react';
import loading from './loading.svg';

class Callback extends Component {
  render() {
    const style = {
      position: 'absolute',
      display: 'flex',
      justifyContent: 'center',
      height: '100vh',
      width: '100vw',
      top: 0,
      bottom: 0,
      left: 0,
      right: 0,
      backgroundColor: 'white',
    }

    return (
      <div style={style}>
        <img src={loading} alt="loading"/>
      </div>
    );
  }
}

export default Callback;
```

The Auth file looks as follows : 

```
import history from '../history';
import auth0 from 'auth0-js';
import { AUTH_CONFIG } from './auth0-variables'; // where we specify our credentials for the the use of Auth0

export default class Auth {
  auth0 = new auth0.WebAuth({
    domain: AUTH_CONFIG.domain,
    clientID: AUTH_CONFIG.clientId,
    redirectUri: AUTH_CONFIG.callbackUrl,
    audience: `https://${AUTH_CONFIG.domain}/userinfo`,
    responseType: 'token id_token',
    scope: 'openid'
  });

  constructor() {
    this.login = this.login.bind(this);
    // we bind the functions which are later described to this instance by using this and bind
    this.logout = this.logout.bind(this);
    this.handleAuthentication = this.handleAuthentication.bind(this);
    this.isAuthenticated = this.isAuthenticated.bind(this);
  }

  login() {
    this.auth0.authorize();
  }

  handleAuthentication() {
    this.auth0.parseHash((err, authResult) => {
      if (authResult && authResult.accessToken && authResult.idToken) {
        this.setSession(authResult);
        history.replace('/feed');
      } else if (err) {
        history.replace('/feed');
        console.log(err);
        alert(`Error: ${err.error}. Check the console for further details.`);
      }
    });
  }

  getAccessToken() {
    const accessToken = localStorage.getItem('access_token'); // we find the value with that key
    if (!accessToken) {
      return new Error('No access token found');
    }
    return accessToken; 
  }

  setSession(authResult) {
    // Set the time that the access token will expire at
    let expiresAt = JSON.stringify((authResult.expiresIn * 1000) + new Date().getTime());
    localStorage.setItem('access_token', authResult.accessToken);
    localStorage.setItem('id_token', authResult.idToken);
    localStorage.setItem('expires_at', expiresAt);
    // navigate to the home route
    history.replace('/feed');
  }

  logout() {
    // Clear access token and ID token from local storage
    localStorage.removeItem('access_token');
    localStorage.removeItem('id_token');
    localStorage.removeItem('expires_at');
    // navigate to the home route
    history.replace('/home');
  }

  isAuthenticated() {
    // Check whether the current time is past the 
    // access token's expiry time
    let expiresAt = JSON.parse(localStorage.getItem('expires_at'));
    return new Date().getTime() < expiresAt;  // which returns a boolean
  }
}

```

Net we add the routes to the application.

```
import React from 'react';
import { Route, Router } from 'react-router-dom';
import App from './App';
import Contact from './Contact';
import About from './About';
import Feed from './Feed';
import Callback from './Callback/Callback';
import Auth from '../Auth/Auth';
import history from '../history';

const auth = new Auth();

const handleAuthentication = (nextState, replace) => {
  if (/access_token|id_token|error/.test(nextState.location.hash)) {
    auth.handleAuthentication();
  }
}

export const makeMainRoutes = () => {
  return (
      <Router history={history} component={App}>
        <div className="container">
          <Route path="/" render={(props) => <App auth={auth} {...props} />} />
          <Route path="/feed" render={(props) => <Feed auth={auth} {...props} />} />
          <Route path="/about" render={(props) => <About auth={auth} {...props} />} />
          <Route path="/contact" render={(props) => <Contact auth={auth} {...props} />} />
          <Route path="/callback" render={(props) => {
            handleAuthentication(props);   
            return <Callback {...props} /> 
          }}/>
        </div>
      </Router>
  );
}

```
We also have an `index.js` file as follows : 

```
import ReactDOM from 'react-dom';
import { makeMainRoutes } from './components/routes';

const routes = makeMainRoutes();

ReactDOM.render(routes, document.getElementById('root'));
```

Next we decribe below the app component :

```
// @flow
import React, { Component } from 'react';
import { Link } from 'react-router-dom';
import Jumbotron from './Jumbotron';
import './App.css';

class App extends Component {
  constructor(props) {
    // calling the constructor of the super class too
    super(props);
    // we can specify with details the state of the class with key value pair
    this.state ={
      jumbotronTitle: "List of courses",
    }
  }

  goTo(route) {
    // meaining you input the variable into the end of the html link
    this.props.history.replace(`/${route}`)
  }

  login() {
    this.props.auth.login();
  }

  logout() {
    this.props.auth.logout();
  }

  render() {
    const { isAuthenticated } = this.props.auth;
    return (
      <div>
        {
          // in the below we return the div only if the user it not authenticated or authenticated repsectively
          !isAuthenticated() && (
            <div>
              <div className="header">
                <ul className="nav nav-pills pull-right">
                    // here we have a link which when clicked lunches the login function
                    // this login function we bind to the current instance
                    <li className="btn btn-primary" onClick={this.login.bind(this)}>Log in</li>
                </ul>
                <h3 className="text-muted">Securing React</h3>
              </div>
              <Jumbotron title={this.state.jumbotronTitle} />
            </div>
          )
        }
        {
          // suppose now that the user is authenticated
          isAuthenticated() && (
            <div>
              <div className="header">
                <ul className="nav nav-pills pull-right">
                // here we have a link which when clicked redirects us to an html link with feed written at the end
                <li><a onClick={this.goTo.bind(this, 'feed')}>Home</a></li>
                <li><Link to="/about">About</Link></li>
                <li><Link to="/contact">Contact</Link></li>
                    <li className="btn btn-primary" onClick={this.logout.bind(this)}>Log out</li>
                </ul>
                <h3 className="text-muted">Securing React</h3>
              </div>
              <Jumbotron title={this.state.jumbotronTitle} />
            </div>
          )
        }
      </div>
    )
  }
}

export default App;
```

Before working on the feed component we install some dependencies :

```
npm install --save auth0-js axios history  jwt-decode
```

Below we also include the code for the Feed component :

```
import React, { Component } from 'react';
import axios from 'axios';
import FeedItem from './FeedItem';

class Feed extends Component {
  constructor(props) {
    super(props);
    this.state = {
      // initially then ourfeed matrix is just an empty matrix
      feeds: [],
    };
  }

  componentWillMount() {
    const { getAccessToken } = this.props.auth;
    // below we have a string and we input the access token
    const headers = { 'Authorization': `Bearer ${getAccessToken()}`}
    const url = 'http://localhost:4000/courses';
    // promise based http client for the browser and node.js
    // it makes it easy to send asynchronous http requests for rest endpoints and perform crud operations
    return axios.get(url, { headers})
      .then(response => this.setState({ feeds: response.data }));
      // the then specifies it's a promise, we assing a new variable called feeds which is the data associated to respond
  }

  login() {
    this.props.auth.login();
  }

  render() {
    const { isAuthenticated } = this.props.auth;

    return (
      <div>
      {
        // here we return the div if the person is not authenticated
        !isAuthenticated() && (
          <h4>
            You are not logged in! Please {' '}
            <a
              style={{ cursor: 'pointer'}}
              // you have this function which is bound to the link
              onClick={this.login.bind(this)}
            >Log in</a>
            {' '}to continue.
          </h4>
        )
      }
      {
        isAuthenticated() && (
          this.state.feeds.map((item) => 
          <FeedItem key={item.id} feed={item} />
          // you render this component if authenticated, we have the component key is the item id
          // the feed variable is initiated to be the item
        )
        )
      }
    </div>
    )
  }
}

export default Feed; 
```

Now we will secure server API files. First we need to run the following commands :

```
npm install --save express-jwt-authz
```
The code is below :

```
import jwtAuthz from 'express-jwt-authz'
```

And we have :

```
const secureApi = jwt({
  secret : jwks.expressJwtSecret({
    cache : true,
    rateLimit : true,
    jwksRequestsPerMinute : 5,
    jwksUri : "https://mannydesigns.auth0.com/.well-known/jwks.json"
  }),
  audience : 'https://manny-linkedin',
  issuer : "https://mannydesigns.auth0.com/",
  algorithms : ['RS256']
});

const checkScopes = jwtAuthz(['read:courses']);

app.get('/courses', secureApi, checkScopes, (req, res) => {
  let courses = { ... }
})
```
