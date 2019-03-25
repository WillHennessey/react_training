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
## Calling this.setState() from another function
In React, whenever you define an event handler that uses `this`, you need to add `this.methodName = this.methodName.bind(this)` to your constructor function.
You can’t call `this.setState()` from inside of the render function!
Any time that you call `this.setState()`, `this.setState()` AUTOMATICALLY calls `.render()` as soon as the state has changed.
Think of `this.setState()` as actually being two things: `this.setState()`, immediately followed by `.render()`.
That is why you can’t call `this.setState()` from inside of the `.render()` method! `this.setState()` automatically calls `.render()`. If `.render()` calls `this.setState()`, then an infinite loop is created.
```jsx
import React from 'react';
import ReactDOM from 'react-dom';

const green = '#39D1B4';
const yellow = '#FFD712';

class Toggle extends React.Component {
  constructor(props) {
    super(props);
    this.state = { color: green };
    this.changeColor = this.changeColor.bind(this);
  }
  
  changeColor() {
    const newColor = this.state.color == green ? yellow : green
    this.setState({color: newColor})
  }
  
  render() {
    return (
      <div style={{background: this.state.color}}>
        <h1>
          Change my color
        </h1>
        <button onClick={this.changeColor}>
          Change color
        </button>
      </div>
    );
  }
}

ReactDOM.render(<Toggle />, document.getElementById('app'));
```
