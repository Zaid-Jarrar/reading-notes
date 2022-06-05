# Reading 37 - React 1

All of the materials are review for REACT JS (which I have forgotten).

## Class Constructor Functions 

ie. ES5:

```js script
function Func(a, b) {
  this.a = a
  this.b = b
}

Func.prototype.getSum = function () {
  return this.a + this.b
}

var x = new Func(3, 4)
```

ie: ES6:

```js script
class Func {
  constructor(a, b) {
    this.a = a
    this.b = b
  }

  getSum() {
    return this.a + this.b
  }
}

let x = new Func(3, 4)
```

returns 7

## Spread syntax

```js script
let arr1 = [1, 2, 3]
let func = (a, b, c) => a + b + c

console.log(func(...arr1)) // 6
```

arrow functions are a shorter way of formulating function expressions

## Callback functions

class implementation on top of constructor based functions

```js script
let doSecond = () => {
  console.log('Do second.')
}

let doFirst = new Promise((resolve, reject) => {
  setTimeout(() => {
    console.log('Do first.')

    resolve()
  }, 500)
})

doFirst.then(doSecond)
```

- example could be made with burgers
- make the order (from the customer)
  promise that you will make the burger
- take the order
- get ingredients
- make the burger
- deliver the burger (end of the promise and callback)

## JSX

```js script
const element = React.createElement(
  'h1',
  {className: 'greeting'},
  'Hello, world!'
);
```

creates an element with the h1 tags (with Babel language) and returns a greeting of hello world.

## Rendering Elements

``html
  <div id="root"></div>
```

this is a root DOM because all contents inside it will be managed by the React DOM.

To render a React element:

-pass DOM element to `ReactDOM.createRoot()`

-then pass that element to `root.render()`

```js script
const element = <h1>Hello, world</h1>;
const root = ReactDOM.createRoot(
  document.getElementById('root')
);
root.render(element);
```

React elements are *immutable* (can't change its children or attributes once you create an element). The only way is to update it by creating a new element and passing it to root.render().

## Props

Element represents a user-defined component:

**props** - single object that has attributes and children passed down to it.

```js script
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

const element = <Welcome name="Sara" />;
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(element);
```

- We call root.render() with the <Welcome name="Sara" /> element.

- React calls the Welcome component with {name: 'Sara'} as the props.

- Our Welcome component returns a <h1>Hello, Sara</h1> element as the result.

- React DOM efficiently updates the DOM to match <h1>Hello, Sara</h1>.

## State

```js script
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}
```

Essentially you create a constructor function that contains state which you can then pass down to other functions as state. After passing it down to its child, an subsequent item you wish to pass down must be in props.

## Tailwind

**tailwind** - style elements by applying pre-existing classes directly to html.

```html
<div class="p-6 max-w-sm mx-auto bg-white rounded-xl shadow-lg flex items-center space-x-4">
  <div class="shrink-0">
    <img class="h-12 w-12" src="/img/logo.svg" alt="ChitChat Logo">
  </div>
  <div>
    <div class="text-xl font-medium text-black">ChitChat</div>
    <p class="text-slate-500">You have a new message!</p>
  </div>
</div>
```

Tailwind has *flexbox*, *padding*, *max-width*, *margin*, etc utilities.

Essentially the importance of using Tailwind is that you are actually utilizing a predefined design system, so no need to adjust numbers to get your desired rendered page.

## Next.js

**Next.js** - React Framework.Promotes an intuitive page-based routing system. It also:

-provides pre-rendering

-allows for auto code splitting for faster page loads.

-client side routing with optimized prefetching.

-built in CSS and Sass support

-API routes

-is fully extendable.