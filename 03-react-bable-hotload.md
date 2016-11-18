# To have babel hotloader setup so that whenever client side js file changes, front end changes. 

1, install the following
`
npm install --save-dev react-hot-loader webpack-hot-middleware
npm install --save-dev babel-preset-stage-2 webpack-dev-server
npm install --save babel-core
`

2, update webpack.dev.config.js file 

* Add webpack-hot-middleware
* add plugin
`
import path from 'path';
import webpack from 'webpack';

export default {
	devtools: 'eval-source-map',
	entry: [
		'webpack-hot-middleware/client',
		path.join(__dirname, '/client/index.js')
	],
	output:{
		path: '/',
		publicPath: '/'
	},
	plugins: [
	    new webpack.NoErrorsPlugin(),
	    new webpack.optimize.OccurenceOrderPlugin(),
		new webpack.HotModuleReplacementPlugin()
	],
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