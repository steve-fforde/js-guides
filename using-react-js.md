## What is React.JS

React is a javascript on open-source front-end library maintained by Facebook, which allows you to create responsive UI more easily, by incorporating HTML like elements directly into your code.

When combined with Redux this makes UI design simpler, as it can produce UI that respond automatically to changes in your data without needing any code to explicitly process and handle the change.

## What is Webpack

Webpack is a tool which will 'hot-load' your website so that you do not need to restart your website after each change and navigate to the correct page.

It will instead remember the current state of your application and load the new code around it, making it much easier to make changes on the fly and see what the results are.

## Prerequisites

You should have the following software installed to use this guide.
* [Node.JS](https://nodejs.org/en/download/) 
* [Visual Studio Code](https://code.visualstudio.com/download)
* [React Developer Tools Chrome Extension](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en)

Follow [Stuart Barlow's Guide to creating a simple express server](https://gitlab.ros.gov.uk/BarlowS/guides/-/blob/master/simple-express-server.md)

> **NB** this guide is written for Linux though much of instructions will  be the same for a window user.
## Instructions

From the terminal, navigate to your project folder, and run the following to install webpack
`npm install --save-dev webpack webpack-dev-server webpack-cli`

`npm install --save react react-dom react-scripts`

The webpack-dev-server will replace the basic express server so you can uninstall it.
`npm uninstall express`

React applications use a very basic html page which it then attaches content to, the webpack server is designed to handle this approach, so in the `public` create a `index.html` file, and add the following content
```html
<!DOCTYPE  html>
<html>
	<head>
		<title>My React App</title>
	</head>
	<body>
		<div  id="react-container"></div>
		<script  src="assets/bundle.js"></script>
	</body>
</html>
```
Now you need to provide webpack with a configuration file so that it knows how to serve your website, you should create this file in your root project directory, called `webpack.conf.js` and add the following content
```js
var path = require("path")
module.exports = {
	mode:  "development",
	entry:  "./index.js",
	output: {
		path:  path.resolve(__dirname, "public"),
		filename:  "bundle.js",
		publicPath:  "/assets/"
	},
	devServer: {
		inline:  true,
		contentBase:  "./public",
		port:  3000
	}
}
```

You will need to launch the webpack server using a more complex command than before, but npm provides a mechanism to make this easier, in your `package.json` file these is a dict called `scripts` this will already contain an entry with the key "test", you can remove this and replace it with a "start" entry, this will allow you to start your server using the command `npm start`
```json
...
	"scripts": {
		"start": "./node_modules/.bin/webpack-dev-server"
	},
...
```

Finally we need to refactor the `index.js` file.
```js
import  React  from  "react"
import  ReactDOM  from  "react-dom"

ReactDOM.render(
	React.createElement("h1", null, "Hello World"),
	document.getElementById("react-container")
)
```

## The Result 

Run `npm start` in your project directory.

You can now navigate to your website at [http://localhost:3000](http://localhost:3000) and you will see the React Component "Hello World" being presented.

Do not stop your server but go back to your code (put the windows side by side if you can) and edit the index.js, for example change the third parameter of the createElement from "Hello World" to "Hello Steve", save the edit, and you will imediately see the change reflected in the web-browser. 
