# React basic and enviroment setup

A simple server can serve HTML is up. Next Step: get basic React component working!
1, create client folder and index.js ( main file for react handler)

`mkdir client`
`touch client/index.js`

in index.js, is pretty standard react stuff: 

`
import React from 'react';
import {render} from 'react-dom';
import App from './components/app';

render(<App />, document.getElementById('app'));

`

2, Pin React root render to HTML which is served in express server

open index.html under server folder

Change body to 

`
<body>
	<div id="app"></div>
	<script src="bundle.js"></script>
</body>

`
explaination is we are going to use webpack to compile all the react file and generate a bundle.js file. 
all html handler need to do is to grab bondle.js and pin that to the div with id 'app' ( or sometimes people like to make it as 'root'). 

3,  Now from server serve index.html--> (pin bundle.js to div with id="app") --> We need to write react js files to generate the bundle.js that index.html can use <--- keep in mind, that we need webpack to compile our all react design file here!

The root react js file is client/index.js as above. notice it is import file ./components/app.js
we need to create file under folder client/components/app.js

in app.js
it is the most standard react syntax

`
import React from 'react';

export default ()=>{
	return(
		<h1> Hello from React</h1>
		);
}
`

4, Environment setup to make our react component to show up 

* install react react-dom

`npm install --save react react-dom `

* express server need to have a middleware : webpack to be able to compile all the js file into bundle.js

add webpack reference in server file server/index.js

`
import webpack from 'webpack';
import webpackMiddleware from 'webpack-dev-middleware';
import webpackConfig from '../webpack.config.dev';
`

also add middleware at the following location

`
let app = express();

 app.use(webpackMiddleware(webpack(webpackConfig)));
 
 app.get("/*", (req,res)=>{
 	res.sendFile(path.join(__dirname, './index.html'));
 });

`

* make webpack comfortable


`
npm install --save-dev webpack webpack-dev-middleware
`

config webpack :

under root directory


`touch webpack.config.dev.js`

content of webpack.config.dev.js


`

import path from 'path';
export default {
	devtools: 'eval-source-map',  
	entry: path.join(__dirname, '/client/index.js'),
	output:{
		path: '/'
	},
	module: {
		loaders: [
			{
				test: /\.js$/,
				include: path.join(__dirname, 'client'),
				loaders: ['babel']
			}
		]
	},
	resolve: {
		extentions: ['', '.js']
	}
}

`


Here are the notes to understand webpack config file:
entry: source file to compile  (MUST HAVE)
output: can give any path, because middleware will serve the bundle from memory instead of serve the actual file

Webpack doesn't know anything about javascript, therefore we need babel. 

that's why we have defined module, which is a object , where we have loaders.
loaders is an array of object

in the first object, specify test: any file with js at the end
include : files in the path will load in to loader
loader : use babel as loader

resolve: anyfile without extension or with .js extension <---HERE, I need more digging of webpack config, but will do that later

install babel loader --> for webpack to understand javascript

`npm install --save-dev babel-loader`

Now the server still fail because babel it self doesn't understand react

need to modify .babelrc file, add 'react' in the preset array


`{
	"presets" : ["es2015", 'react']
}`


and install the preset

`npm install --save-dev babel-preset-react`

Now we are all good 

finally add 

`devtools: 'eval-source-map' `

for debugging purpose. 

