#Finally, Redux, Really?

Credit goes to a seriese of video
https://www.youtube.com/watch?v=BVvBa18o8Es


## Let's start by telling a Love Story of Store and Reducer!

Store and Reducer is married. What does that mean? 

Every Store when it was born, God give it a Reducer, just for that Store, and give it an initial state.
 
This is why ```const store = createStore(Reducer, initial-state); ```
where ```import { createStore } from redux ```

OK, What do the married couple do everyday?

Store is a guy, who is lazy, only thing he does is to hold a thing, called "state". He is so lazy, that he always tell his wife, Reducer what the state is, so we can see there is a straight wire from state inside store to the Reducer. Basically, Store always shout to Reducer " Hey, This is what I have! as I am not hiding anything from you!"

Then Reducer has the power to change the state inside the store. She will do it when she sees a Request from other people, what a traitor! However, Reducer has a very bad vision, that she cannot see the Request(letter) unless she has her glasses on. But when she sees the Request, she will immediately change the state inside the store according to a Recipe. 

Luckily, Store, the husband has the control of when Reducer will have her glasses and be able to do something with Store's state. The moment when Store let Reducer sees the Request, is called "dispatch", which is a built-in function/feature Store has. And We as a Programer, give the Requests a Unique Name: "Action". 

Since I am from a hardware background, I would use digital circuit to descript the relationship of Store and Reducer. It will be look like this


```

	Action
	  |   _____________________  
	  V  |                     |
	  |  V                     |
	 ( AND )                   ^
	    |     ____________     | Dispatch
	    |    |   State  __|____|________
	  __v____V___      |                |  Subscribe
	 |  Reducer  |     |Store  {State}  |--->-----------(Call-back-Functions get called whenever state changes! )
	 |___________|     |________________|
	       |                       ^
	       V_______________________|
	                 New State



```

Oh, forgot to mention, Store has a bad habit that he will broadcast to nosy neighbores whenever the state inside him changes. Who knows what all the nosy neighbores will do to this couple?! This bad habit, is called "Subscribe", and it is a native feature of the Store.

## Let's then make state immutable

Well, Reducer has two ways to change the state inside Store. 1, take the what Store gives her, change it, and give it back to Store. 2, take what Store gives her, meh, don't like it, too old, Reducer decide to make a copy of the state, and change it, give the new state back to Store. 

So, it is important to understand that, the "immutable" and "create new state every time change state" process is done by the Wife- Reducer, that reminds us, as Programer, to do something special in the Reducer to make sure it always create a new object whenever Reducer works her job. 

Some Notes taken here

1, spread operator from ES6, ```...state``` means spreading the state, always put this in the first, and then add the update part of the state, so that the new declaration of the that updated properties/keys of that part of the state will take the most latter statement and overwrite the initial spread operator that laied out that old value of that part of the state.  examples:

```
const reducer = (state=initialState, action) => {
	switch (action.type) {
		case "ADD":
			state={
				...state,
				result: state.result + action.payload,
				lastValues: [...state.lastValues, action.payload]
		    };
	    	break;
		case "SUBSTRACT":
			state={
				...state,
				result: state.result - action.payload,
				lastValues: [...state.lastValues, action.payload]
		    };
	    	break;
	}
	return state;
};


```

2, Also since Reducer here initialized state by taking advantage of ES6 syntax, the born process of Store is simpler, ``` store = createStore(reducer); ```

Again, Store married Reducer, passing Reducer the initial state is the same passing it to Store, fair. 

