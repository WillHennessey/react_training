# React Notes
## propTypes
propTypes are useful for two reasons. The first reason is prop validation.

Validation can ensure that your `props` are doing what they’re supposed to be doing. If `props` are missing, or if they’re present but they aren’t what you’re expecting, then a warning will print in the console.

This is useful, but reason #2 is arguably more useful: documentation.

Documenting `props` makes it easier to glance at a file and quickly understand the component class inside. When you have a lot of files, and you will, this can be a huge benefit.

The first step to making a propType is to search for a property named propTypes on the instructions object. If there isn’t one, make one! You will have to declare it after the close of your component declaration, since it will be a static property.

```jsx
import React from 'react';

export class MessageDisplayer extends React.Component {
  render() {
    return <h1>{this.props.message}</h1>;
  }
}

// This propTypes object should have
// one property for each expected prop:
MessageDisplayer.propTypes = {
  message: React.PropTypes.string
};
```

If you add .isRequired to a propType, then you will get a console warning if that prop isn’t sent.

```jsx
import React from 'react';

export class Runner extends React.Component {
  render() {
  	let miles = this.props.miles;
    let km = this.props.milesToKM(miles);
    let races = this.props.races.map(function(race, i){
      return <li key={race + i}>{race}</li>;
    });

    return (
      <div style={this.props.style}>
        <h1>{this.props.message}</h1>
        { this.props.isMetric && 
          <h2>One Time I Ran {km} Kilometers!</h2> }
        { !this.props.isMetric && 
          <h2>One Time I Ran {miles} Miles!</h2> }
        <h3>Races I've Run</h3>
        <ul id="races">{races}</ul>
      </div>
    );
  }
}

Runner.propTypes = {
  message:   React.PropTypes.string.isRequired,
  style:     React.PropTypes.object.isRequired,
  isMetric:  React.PropTypes.bool.isRequired,
  miles:     React.PropTypes.number.isRequired,
  milesToKM: React.PropTypes.func.isRequired,
  races:     React.PropTypes.array.isRequired
};
```

## PropTypes in Stateless Functional Components

To write propTypes for a stateless functional component, you define a propTypes object as a property of the stateless functional component itself.
Here’s what that looks like:
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

GuineaPigs.propTypes = {
  src: React.PropTypes.string.isRequired
}
```
