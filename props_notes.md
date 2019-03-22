# React Notes
## this.props
Information that gets passed from one component to another is known as “props.”
Non string props must be passed in using curly braces, for example `<MyObject stringProp="a string" otherProp={1}>`
Heres an example of passing in a prop and accessing it.
```jsx
import React from 'react';
import ReactDOM from 'react-dom';

class PropsDisplayer extends React.Component {
  render() {
  	const stringProps = JSON.stringify(this.props);

    return (
      <div>
        <h1>CHECK OUT MY PROPS OBJECT</h1>
        <h2>{stringProps}</h2>
      </div>
    );
  }
}

ReactDOM.render(<PropsDisplayer myProp="Hello"/>, document.getElementById('app'));
```
## Pass an event handler as a prop
Event handlers are defined as methods within a component.
Here I've defined a talk method and passed it to the button component as a prop named `talk`
```jsx
import React from 'react';
import ReactDOM from 'react-dom';
import { Button } from './Button';

class Talker extends React.Component {
  talk() {
    let speech = '';
    for (let i = 0; i < 10000; i++) {
      speech += 'blah ';
    }
    alert(speech);
  }
  
  render() {
    return <Button talk={this.talk}/>;
  }
}

ReactDOM.render(
  <Talker />,
  document.getElementById('app')
);
```
Now the button component can use the prop talk as an event handler within itself.
```jsx
import React from 'react';

export class Button extends React.Component {
  render() {
    return (
      <button onClick={this.props.talk}>
        Click me!
      </button>
    );
  }
}
```
## this.props.childern
In Example 1, `<BigButton>`‘s `this.props.children` would equal the text, “I am a child of BigButton.”
In Example 2, `<BigButton>`‘s `this.props.children` would equal a <LilButton /> component.
In Example 3, `<BigButton>`‘s `this.props.children` would equal undefined.
If a component has more than one child between its JSX tags, then `this.props.children` will return those children in an array.
However, if a component has only one child, then `this.props.children` will return the single child, not wrapped in an array.
```jsx
import React from 'react';
import { LilButton } from './LilButton';

class BigButton extends React.Component {
  render() {
    console.log(this.props.children);
    return <button>Yo I am big</button>;
  }
}


// Example 1
<BigButton>
  I am a child of BigButton.
</BigButton>


// Example 2
<BigButton>
  <LilButton />
</BigButton>


// Example 3
<BigButton />
```
## .defaultProps
If a component expects a prop and it is not provided, you can declare defaultProps that will be used instead.

```jsx
import React from 'react';
import ReactDOM from 'react-dom';

class Button extends React.Component {
  render() {
    return (
      <button>
        {this.props.text}
      </button>
    );
  }
}

// defaultProps goes here:
Button.defaultProps = { text: 'I am a button' };

ReactDOM.render(
  <Button >, 
  document.getElementById('app')
);
```
