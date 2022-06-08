# Reading 38 - React 2

## Conditional Rendering

- works same as JavaScript by using operators like if or the conditional operator to create elements displaying current state.

```js script
function UserGreeting(props) {
  return <h1>Welcome back!</h1>;
}

function GuestGreeting(props) {
  return <h1>Please sign up.</h1>;
}
```

### Element Variables

Store elements using variables

```js script
class LoginControl extends React.Component {
  constructor(props) {
    super(props);
    this.handleLoginClick = this.handleLoginClick.bind(this);
    this.handleLogoutClick = this.handleLogoutClick.bind(this);
    this.state = {isLoggedIn: false};
  }

  handleLoginClick() {
    this.setState({isLoggedIn: true});
  }

  handleLogoutClick() {
    this.setState({isLoggedIn: false});
  }

  render() {
    const isLoggedIn = this.state.isLoggedIn;
    let button;
    if (isLoggedIn) {
      button = <LogoutButton onClick={this.handleLogoutClick} />;
    } else {
      button = <LoginButton onClick={this.handleLoginClick} />;
    }

    return (
      <div>
        <Greeting isLoggedIn={isLoggedIn} />
        {button}
      </div>
    );
  }
}

ReactDOM.render(
  <LoginControl />,
  document.getElementById('root')
);
```

Renders either a login or logout button depending on the conditional.

### Inline If-Else with Conditional Operator

Another method for conditionally rendering elements inline is to use the JavaScript conditional operator `condition ? true : false.`

### Keys

**Keys** - lets React know which items have changed, added, or removed. Should also be given to the elements inside the array.

```js script
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number) =>
  <li key={number.toString()}>
    {number}
  </li>
);
```

Keys must only be unique among siblings. But they don't need to be *globally unique*.

## Forms

```js script
class NameForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {value: ''};

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({value: event.target.value});
  }

  handleSubmit(event) {
    alert('A name was submitted: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Name:
          <input type="text" value={this.state.value} onChange={this.handleChange} />
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```

Create a constructor function that also has state, which will be passed down to different elements.

Create a handle submit function and pass it down using 'this'.

### Handle Multiple Inputs

Multiple controlled `input` elements = control them by adding a `name` attribute to each target.

- **setState()** - merges a partial state into the current state.

## Lifting State

- REACT can call a function, `onChange`, on the Document Object Model `<input>`.

- `onChange` transforms into `handleChange` method when passed down. The current Component will call the prop with the new desired value. This value would be provided by its parent component.

- two input methods can be created depending on the user input and various dependencies.

- Current component can request REACT to re-render itself by calling `setState()`, with new input value and the current input.

## Composition vs Inheritance

**Composition** - specific component generates a *generic* component and configures it with props.

**Inheritance** - avoid. New users use this but it is better to use *composition*.

```js script
function Dialog(props) {
  return (
    <FancyBorder color="blue">
      <h1 className="Dialog-title">
        {props.title}
      </h1>
      <p className="Dialog-message">
        {props.message}
      </p>
    </FancyBorder>
  );
}

function WelcomeDialog() {
  return (
    <Dialog
      title="Welcome"
      message="Thank you for visiting our spacecraft!" />
  );
}
```

## Containment

-use `children` prop to pass children's elements into their output.

```js script
function FancyBorder(props) {
  return (
    <div className={'FancyBorder FancyBorder-' + props.color}>
      {props.children}
    </div>
  );
}
```

## Thinking in React

Step 1: Break The UI Into A Component Hierarchy

Step 2: Build A Static Version in React

Step 3: Identify The Minimal (but complete) Representation Of UI State

Step 4: Identify Where Your State Should Live

Step 5: Add Inverse Data Flow