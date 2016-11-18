#Simple Env setup to run express server

1, clean folder

`npm init`

2, create server file

`mkdir server`
`touch index.js`

in the index.js, the following is to setup a basic express server
`
import express from 'express';
 let app = express();

 app.get("/*", (req,res)=>{
 	res.send('hello world');
 });

 app.listen(3000, ()=> console.log('Running on localhost:3000'));

`
open package.json, 
add 
`
"scripts": {
    "server": "babel-node server/index.js",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
`

Install express 

`npm install --save express`

Install babel-cli 
`npm install --save-dev babel-cli`

config babel to recognize es6 syntax
at root folder
touch .babelrc

open .babelrc

`
{
	"presets" : ["es2015"]
}
`
install plugin

`npm install --save-dev babel-preset-es2015`

3, start server

`npm run server`

Now you should have a simple express server running!

4, serve a html page and using nodemon

1, change res.send... 
to 

`res.sendFile(path.join(__dirname, './index.html'));`

Then create a boilerplate HTML index.html under folder server/

`
<!DOCTYPE html>
<html lang='en'>
<head>
	<meta charset="UTF-8">
	<title>Red Dice</title>
	<meta content="width-device-width, initial-scale=1" name="viewpoint" />
</head>	

<body>
	<h1>Hello World!!!</h1>
</body>
</html>	
`

install nodemon to enable realtime refresh server whenever server folder changes ( BUT NOT CLIENT side, which will use webpack!)

`npm install nodemon`

in packedge.json

`"server": "nodemon --watch server --exec babel-node -- server/index.js",`




