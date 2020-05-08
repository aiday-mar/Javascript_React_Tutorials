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

The OWASP project also named : Open Web Application Security Project. It contains references to potential attacks on the internet. Cross-site scripting (XSS) attacks, is when a malicious script is injected into a trusted site. Some example of attacks have been pulling data from cookies, session tokens, and all kinds of sensitive information. When you use for example the keyword `dangerouslySetInnerHTML`, this leaves our code vulnerable to attacks.
