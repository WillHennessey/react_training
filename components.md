# React Notes
## Creating Components
React applications are made out of components.
A component is a small, reusable chunk of code that is responsible for one job. That job is often to render some HTML.
```jsx
import React from 'react';
import ReactDOM from 'react-dom';

class MyComponentClass extends React.Component {
  render() {
    return <h1>Hello world</h1>;
  }
};

ReactDOM.render(<MyComponentClass />, document.getElementById('app'));
```
Component class variable names must begin with capital letters!
A render method is a property whose name is render, and whose value is a function. The term “render method” can refer to the entire property, or to just the function part.
A render method must contain a `return` statement. Usually, this `return` statement returns a JSX expression.
```jsx
import React from 'react';
import ReactDOM from 'react-dom';

class QuoteMaker extends React.Component {
  render() {
    return (
      <blockquote>
      <p>
        What is important now is to recover our senses.
      </p>
      <cite>
        <a target="_blank" 
          href="https://en.wikipedia.org/wiki/Susan_Sontag">
          Susan Sontag
        </a>
      </cite>
    </blockquote>
      );
  }
}

ReactDOM.render(<QuoteMaker/>, document.getElementById('app'));
```

## Using a variable attribute in a component
```jsx
import React from 'react';
import ReactDOM from 'react-dom';


const owl = {
  title: 'Excellent Owl',
  src: 'https://s3.amazonaws.com/codecademy-content/courses/React/react_photo-owl.jpg'
};

// Component class starts here:
class Owl extends React.Component {
  render () {
    return(
      <div>
        <h1>{owl.title}</h1>
        <img src={owl.src} alt={owl.title}/>
      </div>
    );
  }
}
ReactDOM.render(<Owl/>, document.getElementById('app'));
```
## Render
A `render()` function must have a return statement. However, that isn’t all that it can have.
A `render()` function can also be a fine place to put simple calculations that need to happen right before a component renders. Here’s an example of some calculations inside of a render function.
```jsx
import React from 'react';
import ReactDOM from 'react-dom';

const friends = [
  {
    title: "Yummmmmmm",
    src: "https://s3.amazonaws.com/codecademy-content/courses/React/react_photo-monkeyweirdo.jpg"
  },
  {
    title: "Hey Guys!  Wait Up!",
    src: "https://s3.amazonaws.com/codecademy-content/courses/React/react_photo-earnestfrog.jpg"
  },
  {
    title: "Yikes",
    src: "https://s3.amazonaws.com/codecademy-content/courses/React/react_photo-alpaca.jpg"
  }
];

class Friend extends React.Component {
  render() {
    var friend = friends[0];
    return(
      <div>
        <h1>{friend.title}</h1>
        <img src={friend.src}/>
      </div>
    );
  }
}
ReactDOM.render(<Friend/>, document.getElementById('app'));

```
Using condtionals in a render statement.
Notice that the if statement is located inside of the render function, but before the return statement. This is pretty much the only way that you will ever see an if statement used in a render function.

```jsx
import React from 'react';
import ReactDOM from 'react-dom';

const fiftyFifty = Math.random() < 0.5;

// New component class starts here:
class TonightsPlan extends React.Component {
  render() {
    let result;
    if (fiftyFifty) {
      result = 'out';
    } else {
      result = 'to bed';
    }
    return(<h1>Tonight I'm going {result} WOOO</h1>);
  }
}
ReactDOM.render(<TonightsPlan/>, document.getElementById('app'));
```
## Using `this` in a component
Note that name isn't called with `()` because it is a get method.
```jsx
import React from 'react';
import ReactDOM from 'react-dom';

class MyName extends React.Component {
	
  get name() {
    return 'Will Hennessey';
  }

  render() {
    return <h1>My name is {this.name}.</h1>;
  }
}

ReactDOM.render(<MyName />, document.getElementById('app'));
```
## Using an event listener in a component
In React, you define event handlers as methods on a component class.
```jsx
import React from 'react';
import ReactDOM from 'react-dom';

class Button extends React.Component {
  scream() {
    alert('AAAAAAAAHHH!!!!!');
  }

  render() {
    return <button onClick={this.scream}>AAAAAH!</button>;
  }
}
ReactDOM.render(<Button/>, document.getElementById('app'));
```
