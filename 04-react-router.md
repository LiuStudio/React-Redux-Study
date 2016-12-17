#Take some time to learn about react router

react-router provide all ui routing method for react. 


`import { Router} from 'react-router'`


react router construtor take two input, history and routes


`
//index.js

import routes from './routes';
import { Router, hashHistory } from 'react-router';

<Router history={hashHistory} routes={routes} />

`


1, history , there are three options 
	* hashHistory -- will insert in url with # , usually used for single page application
	* browerHistory --- url in format of www.dummy.com/home/aboutus, need server to be able to response for the url get query
	* 

2, routes, is a JavaScript file that described how the routing is archetectured. 
A good example is 

`

//routes.js

import { Route, IndexRoute } from 'react-router';

export default(
	<Route path="/" component={App} >
		<IndexRoute component={Greeting} />
		<Route path="signup" component={SignupPage} />
		<Route path='login' component={LoginPage} />
		<Route path="aboutus" component={AboutUsPage} />
			<IndexRoute component={HomePage} />
			<Route path="leader" component={LeaderPage} />
			<Route path="product" component={ProductPage} />
	</Route>
)

`

Notes: 
	* when there is a "IndexRoute" , indicate there is a parent to child branching
	* each component has a this.props.children , which refer to the component according to the path that the router arranged.


3, react Router definition usually defined in index.js