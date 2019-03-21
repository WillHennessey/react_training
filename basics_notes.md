# React notes

## Using JSX Elements
You can't use the attribute `class` for JSX elements, you must use `className` which will be converted to class in HTML.
```jsx
import React from 'react';
import ReactDOM from 'react-dom';
const myDiv = <div className="big">I AM A BIG DIV</div>;
ReactDOM.render(myDiv, document.getElementById('app'));
```
In JSX you must include a closing slash (/) for self closing tags like `<br>` or `<img>`
```jsx
const profile = (
  <div>
    <h1>I AM JENKINS</h1>
    <img src="images/jenkins.png"/>
    <article>
      I LIKE TO SIT
      <br/>
      JENKINS IS MY NAME
      <br/>
      THANKS HA LOT
    </article>
  </div>
);
```
## JS injection in JSX
You can execute JS code within a JSX element by adding curly braces around the code.
```jsx
ReactDOM.render(
  <h1>{2 + 3}</h1>, 
  document.getElementById('app')
);
```
A second example.
```jsx
const math = <h1>2 + 3 = {2 + 3}</h1>;
ReactDOM.render(math, document.getElementById('app'));
```
When you inject JavaScript into JSX, that JavaScript is part of the same environment as the rest of the JavaScript in your file.
That means that you can access variables while inside of a JSX expression, even if those variables were declared on the outside.
```jsx
const theBestString = 'tralalalala i am da best';
ReactDOM.render(<h1>{theBestString}</h1>, document.getElementById('app'));
```
When writing JSX it is common to use variables to set attributes.
```jsx
const goose = 'https://s3.amazonaws.com/codecademy-content/courses/React/react_photo-goose.jpg';

const gooseImg = <img src={goose}/>;
ReactDOM.render(gooseImg, document.getElementById('app'));
```
JSX components can have event listeners like HTML elements.
JSX event listeners should be written in camelCase not lowercase.
```jsx
function makeDoggy(e) {
  // Call this extremely useful function on an <img>.
  // The <img> will become a picture of a doggy.
  e.target.setAttribute('src', 'https://s3.amazonaws.com/codecademy-content/courses/React/react_photo-puppy.jpeg');
  e.target.setAttribute('alt', 'doggy');
}

const kitty = (
	<img 
		src="https://s3.amazonaws.com/codecademy-content/courses/React/react_photo-kitty.jpg" 
		alt="kitty" 
    onClick={makeDoggy} />
);

ReactDOM.render(kitty, document.getElementById('app'));
```
## Conditionals
You can not inject an if statement into a JSX expression.
The below example will FAIL.
```jsx
(
  <h1>
    {
      if (purchase.complete) {
        'Thank you for placing an order!'
      }
    }
  </h1>
)
```
This is an example of how to write a conditional with if/else statements
```jsx
function coinToss() {
  // This function will randomly return either 'heads' or 'tails'.
  return Math.random() < 0.5 ? 'heads' : 'tails';
}

const pics = {
  kitty: 'https://s3.amazonaws.com/codecademy-content/courses/React/react_photo-kitty.jpg',
  doggy: 'https://s3.amazonaws.com/codecademy-content/courses/React/react_photo-puppy.jpeg'
};
let img;

// if/else statement begins here:
if (coinToss() === 'heads') {
  img = <img src={pics.kitty}/>;
}
else {
  img = <img src={pics.doggy}/>;
}
ReactDOM.render(img, document.getElementById('app'));
```
You can also use the ternary operator in a JSX expression
```jsx
function coinToss () {
  // Randomly return either 'heads' or 'tails'.
  return Math.random() < 0.5 ? 'heads' : 'tails';
}

const pics = {
  kitty: 'https://s3.amazonaws.com/codecademy-content/courses/React/react_photo-kitty.jpg',
  doggy: 'https://s3.amazonaws.com/codecademy-content/courses/React/react_photo-puppy.jpeg'
};

const img = <img src={pics[coinToss() === 'heads'? 'kitty' : 'doggy']} />;
ReactDOM.render(
	img, 
	document.getElementById('app')
);
```
You can use the `&&` conditional when you want to sometimes do an action
```jsx
const judgmental = Math.random() < 0.5;

const favoriteFoods = (
  <div>
    <h1>My Favorite Foods</h1>
    <ul>
      <li>Sushi Burrito</li>
      <li>Rhubarb Pie</li>
      {!judgmental && <li>Nacho Cheez Straight Out The Jar</li>}
      <li>Broiled Grapefruit</li>
    </ul>
  </div>
);

ReactDOM.render(
	favoriteFoods, 
	document.getElementById('app')
);
```
## Arrays and lists

If you want to create a list of JSX elements, then `.map()` is often your best bet.
```jsx
const people = ['Rowe', 'Prevost', 'Gare'];
const peopleLis = people.map(person => <li>{person}</li>);
ReactDOM.render(<ul>{peopleLis}</ul>, document.getElementById('app'));
```

A key is a JSX attribute. The attribute’s name is key. The attribute’s value should be something unique, similar to an id attribute.

keys don’t do anything that you can see! React uses them internally to keep track of lists.
Not all lists need to have keys. A list needs keys if either of the following are true:
The list-items have memory from one render to the next. For instance, when a to-do list renders, each item must “remember” whether it was checked off. The items shouldn’t get amnesia when they render.
A list’s order might be shuffled. For instance, a list of search results might be shuffled from one render to the next.

Here's an example of using `.map()` with an index to set the keys for `<li>` tags
```jsx
const people = ['Rowe', 'Prevost', 'Gare'];
const peopleLis = people.map((person, i) => <li key={'person_' + i}>{person}</li>);
ReactDOM.render(<ul>{peopleLis}</ul>, document.getElementById('app'));
```
