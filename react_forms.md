# React Notes
## Update an Input's Value
In this example, when a user types or deletes in the `<input />`, then that will trigger a change event, which will call `handleUserInput`.
When the state is changed it'll trigger a `render()` automatically, setting the input value as `this.state.userInput`.

```jsx
import React from 'react';
import ReactDOM from 'react-dom';

export class Input extends React.Component {
  constructor(props) {
    super(props);
    this.state = { userInput: '' };
    this.handleUserInput = this.handleUserInput.bind(this);
  }
  
  render() {
    return (
      <div>
        <input type="text" 
               onChange={this.handleUserInput} 
               value={this.state.userInput} />
        <h1>{this.state.userInput}</h1>
      </div>
    );
  }
  
  handleUserInput(e) {
    this.setState({ userInput: e.target.value });
  }
}

ReactDOM.render(
	<Input />,
	document.getElementById('app')
);
```

## Controlled vs Uncontrolled
There are two terms that will probably come up when you talk about React forms: controlled component and uncontrolled component.
An uncontrolled component is a component that maintains its own internal state. 
A controlled component is a component that does not maintain any internal state.
Since a controlled component has no state, it must be controlled by someone else.
Think of a typical `<input type='text' />` element. 
It appears onscreen as a text box.
If you need to know what text is currently in the box, then you can ask the `<input />`, possibly with some code like this:
```jsx
let input = document.querySelector('input[type="text"]');

let typedText = input.value; // input.value will be equal to whatever text is currently in the text box.
```
The important thing here is that the `<input />` keeps track of its own text. You can ask it what its text is at any time, and it will be able to tell you.
The fact that `<input />` keeps track of information makes it an uncontrolled component. It maintains its own internal state, by remembering data about itself.
A controlled component, on the other hand, has no memory. If you ask it for information about itself, then it will have to get that information through `props`.
Most React components are controlled.

In React, when you give an `<input />` a value attribute, then something strange happens: the `<input />` BECOMES controlled.
It stops using its internal storage. This is a more ‘React’ way of doing things.
