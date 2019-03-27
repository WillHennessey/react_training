# React Notes
## Inline styles
An inline style is a style that’s written as an attribute, like this:
```jsx
<h1 style={{ color: 'red' }}>Hello world</h1>
```
The outer curly braces inject JavaScript into JSX. They say, “everything between us should be read as JavaScript, not JSX.”

The inner curly braces create a JavaScript object literal. They make this a valid JavaScript object:
```jsx
{ color: 'red' }
```

## Make A Style Object Variable
In this example the styles are stored in an object, this removes the need for curly braces.
```jsx
import React from 'react';
import ReactDOM from 'react-dom';
const styles = { background: 'lightblue', color: 'darkred' };

const styleMe = <h1 style={styles}>Please style me! I am so bland!</h1>;

ReactDOM.render(
	styleMe, 
	document.getElementById('app')
);
```

## Style Name Syntax
In regular JavaScript, style names are written in hyphenated-lowercase:
```js
const styles = {
  'margin-top':       "20px",
  'background-color': "green"
};
```

In React, those same names are instead written in camelCase:

```jsx
const styles = {
  marginTop:       "20px",
  backgroundColor: "green"
};
```

### Style value syntax
In regular JS, style values are almost always strings. Even if a style value is numeric, you usually have to write it as a string so that you can specify a unit. For example, you have to write "450px" or "20%".

In React, if you write a style value as a number, then the unit "px" is assumed.

```jsx
const styles = { background: 'lightblue', color: 'darkred', marginTop: 100, fontSize: 50 };
```

### Share Styles Across Multiple Components
One way to make styles reusable is to keep them in a separate JavaScript file. 
This file should export the styles that you want to reuse, via export. 
You can then import your styles into any component that wants them.

```jsx
const fontFamily = 'Comic Sans MS, Lucida Handwriting, cursive';
const background = 'pink url("https://media.giphy.com/media/oyr89uTOBNVbG/giphy.gif") fixed';
const fontSize = '4em';
const padding = '45px 0';
const color = 'green';

export const styles = {
  fontFamily: fontFamily,
  background: background,
  fontSize:   fontSize,
  padding:    padding,
  color:      color
};
```

