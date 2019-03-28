# React Notes
## Mounting lifecycle method
Lifecycle methods are methods that get called at certain moments in a component’s life.

You can write a lifecycle method that gets called right before a component renders for the first time.

You can write a lifecycle method that gets called right after a component renders, every time except for the first time.

You can attach lifecycle methods to a lot of different moments in a component’s life. This has powerful implications!

There are three categories of lifecycle methods: mounting, updating, and unmounting.

A component “mounts” when it renders for the first time. This is when mounting lifecycle methods get called.

There are three mounting lifecycle methods:

* componentWillMount
* render
* componentDidMount

When a component mounts, it automatically calls these three methods, in order.
If you need to do something only the first time that a component renders, then it’s probably a job for a mounting lifecycle method.
 
```jsx
import React from 'react';
import ReactDOM from 'react-dom';

export class Flashy extends React.Component {
  componentWillMount() {
    alert('AND NOW, FOR THE FIRST TIME EVER...  FLASHY!!!!');
  }
  
  componentDidMount() {
    alert('YOU JUST WITNESSED THE DEBUT OF...  FLASHY!!!!!!!');
  }

  render() {
    alert('Flashy is rendering!');

    return (
      <h1 style={{ color: this.props.color }}>
        OOH LA LA LOOK AT ME I AM THE FLASHIEST
      </h1>
    );
  }
}

ReactDOM.render(
  <Flashy color='red' />,
  document.getElementById('app')
);

setTimeout(() => {
  ReactDOM.render(
    <Flashy color='green' />,
    document.getElementById('app')
  );
}, 2000);
```
