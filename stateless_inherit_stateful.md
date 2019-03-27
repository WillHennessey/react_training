# React Notes
## Stateless component inherits from stateful component
Here's an example of Parent.js importing Child.js and passing it's state attribute name to Child.js via the use of props.
### Parent.js
```jsx
import React from 'react';
import ReactDOM from 'react-dom';
import { Child } from './Child';


class Parent extends React.Component {
  constructor(props) {
    super(props)
    this.state = { name: 'Frarthur' }
  }
  
  render() {
    return <Child name={this.state.name}/>;
  }
}

ReactDOM.render(<Parent/>, document.getElementById('app'));
```

### Child.js
```jsx
import React from 'react';


export class Child extends React.Component {
  render() {
    return <h1>Hey, my name is {this.props.name}!</h1>;
  }
  
}
```

**IMPORTANT NOTE:**
A React component should use props to store information that can be changed, but can only be changed by a different component.
A React component should use state to store information that the component itself can change.
