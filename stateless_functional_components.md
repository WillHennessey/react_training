# React Notes
## Stateless Functional Components
If you have a component class with nothing but a render function, then you can rewrite that component class in a very different way. 
Instead of using React.Component, you can write it as a JavaScript function.

A component class written as a function is called a stateless functional component. 
Stateless functional components have some advantages over typical component classes.

## Friend.js as a component class
```jsx
import React from 'react';
import ReactDOM from 'react-dom';

export class Friend extends React.Component {
	render() {
		return <img src='https://s3.amazonaws.com/codecademy-content/courses/React/react_photo-octopus.jpg' />;
	}
}

ReactDOM.render(
	<Friend />,
	document.getElementById('app')
);
```

## Friend.js as a stateless functional component
```jsx
import React from 'react';
import ReactDOM from 'react-dom';

export const Friend = () => {
		return <img src='https://s3.amazonaws.com/codecademy-content/courses/React/react_photo-octopus.jpg' />;
}

ReactDOM.render(
	<Friend />,
	document.getElementById('app')
);
```

## GuineaPigs.js as a component class
```jsx
import React from 'react';

export class GuineaPigs extends React.Component {
  render() {
    let src = this.props.src;
    return (
      <div>
        <h1>Cute Guinea Pigs</h1>
        <img src={src} />
      </div>
    );
  }
}
```

## GuineaPigs.js as a stateless functional component

```jsx
import React from 'react';

export const GuineaPigs = (props) => {
  let src = props.src;
  return (
    <div>
      <h1>Cute Guinea Pigs</h1>
      <img src={src} />
    </div>
  );
}
```
