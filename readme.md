I basically just slightly repackaged this tutorial for usage as a stand alone backend:  
https://www.netlify.com/docs/functions/#tools-for-building-javascript-functions  

This tutorial is a part of this series:  
https://github.com/andrewdownie/netlify-series

## 1) Create a git repo and clone it down
Netlify requires a git repo to deploy from

## 2) In the new git repo, run the commands:
```bash
npm init
```
(all the default are fine for the npm init command)

```bash
npm i netlify-lambda
```

## 3) Create a new file called 'netlify.toml' in the root of your git repo, and fill it with the following:
```toml
[build]
  functions = "./build"
  command = "npm run build"
```

## 4) Create a new folder called 'src' in the root of your git repo, in the src folder, create a new file named 'test.js'. Fill the test.js file with the simplest lambda function:
```js
exports.handler = (event, context, callback) => {
  callback(null, {
    statusCode: 200,
    body: 'your msg here',
    headers: {
      'Access-Control-Allow-Origin': '*'
    }
  })
)
```

## 5) Add a start and build script to the package.json file that runs the corresponding netlify-lambda functions:
```json
"scripts": {
  ...
  "start": "netlify-lambda serve src",
  "build": "netlify-lambda build src"
  ...
}
```

## 6) Add a .gitignore and ignore the node_modules folder and the build folder
```
/node_modules
/build
```

## 7) Add, commit, push everything in your git repo

## 8) Use the netlify web interface to select you git repo and deploy it as a netlify functions service
Once it's deployed, click the green preview button that appears, and append /.netlify/functions/test to the url you are taken to, to see your simple function in action
