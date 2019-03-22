# React Notes
## State
Dynamic information is information that can change.
React components will often need dynamic information in order to render.
For example, imagine a component that displays the score of a basketball game.
The score of the game might change over time, meaning that the score is dynamic.
Our component will have to know the score, a piece of dynamic information, in order to render in a useful way.
There are two ways for a component to get dynamic information: props and state.
Besides props and state, every value used in a component should always stay exactly the same.

Unlike props, a component’s state is not passed in from the outside. A component decides its own state.
To make a component have state, give the component a state property. This property should be declared inside of a constructor method, like this:

`this.state` should be equal to an object.
This object represents the initial “state” of any component instance.
It is important to note that React components always have to call super in their constructors to be set up properly.

State can be read by the component like `{this.props.attribute}` you can use `{this.state.attribute}`

```jsx
import React from 'react';
import ReactDOM from 'react-dom';

class App extends React.Component {
	// constructor method begins here:
  constructor(props) {
    super(props);
    this.state = { title: 'Best App' };
  }
	
  render() {
    return (
      <h1>
        {this.state.title}
      </h1>
    );
  }
}
ReactDOM.render(<App/>, document.getElementById('app'));
```

## Updating state with this.setState()
A component changes its state by calling the function `this.setState()`.

`this.setState()` takes two arguments: an object that will update the component’s state, and a callback. 
You basically never need the callback.
`this.setState()` takes an object, and merges that object with the component’s current state.
If there are properties in the current state that aren’t part of that object, then those properties remain how they were.
```jsx
import React from 'react';

class Example extends React.Component {
  constructor(props) {
  	super(props);
    this.state = {
      mood:   'great',
      hungry: false
    };
  }

  render() {
    return <div></div>;
  }
}

<Example />
```
