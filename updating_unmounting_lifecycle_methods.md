# React Training
## Updating lifecycle methods
The first time that a component instance renders, it does not update. A component updates every time that it renders, starting with the second render.

There are five updating lifecycle methods:

* componentWillReceiveProps
* shouldComponentUpdate
* componentWillUpdate
* render
* componentDidUpdate

Whenever a component instance updates, it automatically calls all five of these methods, in order.

The first updating lifecycle method is called `componentWillReceiveProps`.

When a component instance updates, `componentWillReceiveProps` gets called before the rendering begins.

As one might expect, `componentWillReceiveProps` only gets called if the component will receive `props`:

```jsx
// componentWillReceiveProps will get called here:
ReactDOM.render(
  <Example prop="myVal" />,
  document.getElementById('app')
);

// componentWillReceiveProps will NOT get called here:
ReactDOM.render(
  <Example />,
  document.getElementById('app')
);
```
`componentWillReceiveProps` automatically gets passed one argument: an object called `nextProps`. `nextProps` is a preview of the upcoming `props` object that the component is about to receive.

A common use of `componentWillReceiveProps` is comparing incoming `props` to current `props` or `state`, and deciding what to render based on that comparison.

```jsx
import React from 'react';
import ReactDOM from 'react-dom';
const yellow = 'rgb(255, 215, 18)';

export class TopNumber extends React.Component {
  constructor(props) {
    super(props);

    this.state = { 'highest': 0 };
  }
  
  componentWillReceiveProps(nextProps) {
    if (nextProps.number > this.state.highest){
      this.setState({ highest: nextProps.number });
    }
  }

  render() {
    return (
      <h1>
        Top Number: {this.state.highest}
      </h1>
    );
  }
}

TopNumber.propTypes = {
  number: React.PropTypes.number,
  game: React.PropTypes.bool
};
```

## shouldComponentUpdate

`shouldComponentUpdate` should return either `true` or `false`.

If `shouldComponentUpdate` returns `true`, then nothing noticeable happens.
But if `shouldComponentUpdate` returns `false`, then the component will not update!
None of the remaining lifecycle methods for that updating period will be called, including `render`.

The best way to use `shouldComponentUpdate` is to have it return `false` only under certain conditions.
If those conditions are met, then your component will not update.

`shouldComponentUpdate` automatically receives two arguments: `nextProps` and `nextState`.
It’s typical to compare `nextProps` and `nextState` to the current `this.props` and `this.state`, and use the results to decide what to do.

```jsx
import React from 'react';
import { random } from './helpers';

export class Target extends React.Component {
  
  shouldComponentUpdate(nextProps, nextState) {
    return this.props.number != nextProps.number;
  }
  
  render() {
    let visibility = this.props.number ? 'visible' : 'hidden';
    let style = {
      position: 'absolute',
      left: random(0, 100) + '%',
      top: random(0, 100) + '%',
      fontSize: 40,
      cursor: 'pointer',
      visibility: visibility
    };

    return (
      <span style={style} className="target">
        {this.props.number}
      </span>
    )
  }
}

Target.propTypes = {
  number: React.PropTypes.number.isRequired
};
```
