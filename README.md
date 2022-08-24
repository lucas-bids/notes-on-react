# My notes on React
This repository has all the notes I've taken during the time I've been studying React JS and its ecosystem. It's mostly based on <a href="https://www.udemy.com/course/react-the-complete-guide-incl-redux/#reviews">Maximilian Schwarzmüller's Udemy Course</a>, but has information taken from documentations, YouTube Videos and so on. It's still a work in progress. Hope you enjoy.

# React - The complete guide

## Javascript Refresher

### Primitive Values vs. Reference Values

Primitive values are: [string](https://developer.mozilla.org/en-US/docs/Glossary/String), [number](https://developer.mozilla.org/en-US/docs/Glossary/Number), [bigint](https://developer.mozilla.org/en-US/docs/Glossary/BigInt), [boolean](https://developer.mozilla.org/en-US/docs/Glossary/Boolean), [undefined](https://developer.mozilla.org/en-US/docs/Glossary/undefined), [symbol](https://developer.mozilla.org/en-US/docs/Glossary/Symbol), and [null](https://developer.mozilla.org/en-US/docs/Glossary/Null)

Reference values are: objects, arrays and functions

Primitive values, just as reference values, store data in the memory, with the difference that when copied into another variable, a new space in memory is created and accessed. In reference values, the original value is the one which is accessed, regardless of how many times it has been instanced on another variable. Example:

**Primitive Values:**

```jsx
let age = 30;
let age1 = age; // Pointing to age
console.log(`age = ${age}  age1 = ${age1}`);
age = 31; // Pointing to new address
console.log(`age = ${age}  age1 = ${age1}`);
```

**Output:**

```
age = 30  age1 = 30
age = 31  age1 = 30
```

**Referenced Values**

```jsx
let info = {
Name :"Abc",
Age :10
}
console.log(`Name : ${info.Name} Age : ${info.Age}`);
let info1 = info;
info1.Age = 14; // Change the Age of original object
console.log(`Name : ${info.Name} Age : ${info.Age}`);
```

**Output:**

```
Name : Abc Age : 10
Name : Abc Age : 14
```

### Array Methods

Run like forEach() inside the array, for each element.

[Array methods](https://www.notion.so/8aaa54ecc4a64264b9906e65355e906e)

## Working with components

### Components

Components are the building blocks of React and are divided on different files. Each React component is a regular JS function, that returns a JSX structure, which will then be rendered on the page.

<aside>
🦉 The returned JSX component, cannot have more than **one** root JSX tag. A good workaround is to wrap everything inside a div. Or to use Fragments, as showed later in the course.

</aside>

### Props

Props are dynamic information used inside components. They are quite similar to HTML attributes, and are set to the JSX component tag as attributes. The props can be passed as an array, or fetched with an API. These props will then be passed to the components file and can be further manipulated to the desired output.

**Inside App.js**

```jsx
<ExpenseItem
        title={expenses[0].title}
        amount={expenses[0].amount}
        date={expenses[0].date}
/>
```

<aside>
🦉 There is an ommited expenses array with multiple objects is this example.

</aside>

**Inside ExpenseItem.js**

```jsx
function ExpenseItem(props) {
  return (
    <div className="expense-item">
      <ExpenseDate date={props.date} />
      <div className="expense-item__description">
        <h2>{props.title}</h2>
        <div className="expense-item__price">$ {props.amount}</div>
      </div>
    </div>
  );
}
```

### Props.children

React components can also be wrapped around other components and default JSX. Just as you pass information through attributes to set up specific behaviour on your component, you have to set up your component to receive other components as children. To do that, you have to write the code 

`{props.children}` 

inside the intended JSX tags.

This link have some good examples: 

[https://reactjs.org/docs/composition-vs-inheritance.html](https://reactjs.org/docs/composition-vs-inheritance.html)

## React States

States are React's way of dealing with dynamic information inside the code. It is an object that stores information about the component and can be changed through React Hooks. It is firstly set with a initial value that can be later reset to a new value. The useState is declared in the following way:

```jsx
const [myVariable, setMyVariable] = useState('0');
```

In this case, the `myVariable` has the initial state of `0` . We can set any new value, usually inside handler functions with `setMyVariable('1')` or any other value.

### Event listeners/ Event handlers

React follows the HTML structure to listen to events. For instance:

```html
<button onClick={activateLasersHandler}>Activate Lasers</button>
```

The function `activateLasersHandler()` can be defined before the returned JSX button.

<aside>
🦉 Using "Handler" at the end of the function reminds us that this function is not being called from anywhere else on the code, but on an event. Just a conventional good practice.

</aside>

A list of event listeners that can be used on JSX tags:

[Window Event Attributes](https://www.notion.so/c45c938f7d5940cb84bc3bef04f5f00c)

[Form Events](https://www.notion.so/8e2be115fca445b59e9eb8ec1a12330b)

[Keyboard Events](https://www.notion.so/89d193a9242d40e18cf4cfd8bbacdceb)

[Copy of Keyboard Events](https://www.notion.so/50d426575aca4c80b05e75d9cd5f5af7)

[Drag Events](https://www.notion.so/5f5c7e939bde4c21865b4a604ff66ece)

[Clipboard Events](https://www.notion.so/7f45f711144a4548a1c31ac0bd77f842)

[Media Events](https://www.notion.so/87d6ed6464664d7b934808243093af91)

[Misc Events](https://www.notion.so/e6d3679babb0483f9b4108588eec9f81)

## useState() Hook

The `useState()` Hook is used to set an initial value and further manipulate it inside the JSX component. The useState is declared in the following way (destructured):

```jsx
const [myVariable, setMyVariable] = useState('0');
```

In this case, the `myVariable` has the initial state of `0` . We can set any new value, usually inside handler functions, with `setMyVariable('new-value')` .

### Functional updates

These updates are used when there is the need to **a previously set value**. Its structure goes as follows:

```jsx
onClick={() => setCount(prevCount => prevCount - 1)}
```

This would be a counting button.

## Rendering lists

To render lists in React, a common approach is to take the data from an array and output it using the .map method. The information retrieved from the array can then be passed via props inside the JSX code. Example:

```jsx
{props.items.map((expense) => (
	<ExpenseItem
		title={expense.title}
		amount={expense.amount}
		date={expense.date}
	/>
))}
```

### Inline Conditional Rendering

Inside curly braces, write a condition (true or false) followed by `&&`  and the desired JSX expression to be rendered. Example:

```jsx
render() {
  const count = false;
  return (
    <div>
      { count && <h1>Messages: {count}</h1>}
    </div>
  );
}
```

In this case, the `<h1>` tag will not be rendered, as count is initially set to false.

## Styled Components

It is a React Library and has to be installed. As the name suggests, instead of having general styles stored in css files that can be accessed globally, you store the css styles inside the component, using CSS-in-JS. Example:

**The styled component:**

```jsx
const Button = styled.a`
  /* This renders the buttons above... Edit me! */

  display: inline-block;
  border-radius: 3px;
  padding: 0.5rem 0;
  margin: 0.5rem 1rem;
  width: 11rem;
  background: transparent;
  color: white;
  border: 2px solid white;

  /* The GitHub button is a primary button
    edit this to target it specifically! */
  ${props => props.primary && css`
    background: white;
    color: black;
  `}
`
```

The component can then be used as normal JSX: `<Button />`

<aside>
🦉 The back-ticks `` are part of a new ES6 feature called **tagged template literals**

</aside>

Some advantages of styled components are providing unique class names for the components (avoiding confusion between different class names), making it easier to manage your CSS. It also makes it easier to import your styles across your project.

## React Fragments and Portals

### Fragments

This tool allows us to replace the possibly buggy `<div>` workaround, to render more than one JSX element on a React component. A great example is when, on a table, the <td> elements are rendered as a child of a parent JSX component:

**Parent Table component:**

```jsx
class Table extends React.Component {
  render() {
    return (
      <table>
        <tr>
          <Columns />
        </tr>
      </table>);
  }
}
```

**Child columns component:**

```jsx
class Columns extends React.Component {
  render() {
    return (
      <React.Fragment>
				<td>Hello</td>
				<td>World</td>
			</React.Fragment>
			);
		}
}
```

If, instead of using the `<Fragment>` element, we used a `<div>` element, the resulting HTML would be incorrect, because the `<td>` would end up in the wrong place.

### Portals

Used to “portal” or to transfer a JSX element outside of its component, to another place in the  DOM. It’s usually used when you need different z-index values relationships, such modal as overlays. Example:

```jsx
const ErrorModal = (props) => {
	return (
		<React.Fragment>
			{ReactDOM.createPortal(
				<Backdrop onClick={props.onConfirm} />,
				document.getElementById('backdrop-root')
			)}
		</React.Fragment>
	);
};
```

<aside>
🦉 The “createPortal” syntax has two arguments: the first, is the JSX element itself, which will be rendered on the location stated on the second argument, in this case the ‘backdrop-root’, declared on the index.js file.

</aside>

This tool enables the backdrop to be rendered outside of all other JSX elements, as it should be, since it “covers” the entire page. It is semantically better to use a portal, in this scenario.

### Refs and Forwarding Refs

React refs make it possible for you to directly access the DOM in React. Generally speaking, we can only access the JSX we write on our own, without having access to final HTML DOM that React generates as a final result. This is an important feature to have as you will occasionally need to perform certain actions on the DOM as you develop your React applications.

<aside>
🦉 It is a general rule of thumb to avoid using refs unless you absolutely have to.

</aside>

The most common use cases are to focus input elements, to enable or disable buttons or just to cause some effect on a highly reusable component. In the example below, `FancyButton` uses `React.forwardRef` to obtain the `ref` passed to it, and then forward it to the DOM `button` that it renders:

```jsx
const FancyButton = React.forwardRef((props, ref) => (
  <button ref={ref} className="FancyButton">
    {props.children}
  </button>
));

// You can now get a ref directly to the DOM button:
const ref = React.createRef();
<FancyButton ref={ref}>Click me!</FancyButton>;
```

That way, we can make specific changes on the FancyButton inside its parent component. For example, if we want to animate that button inside only a price table (and not on other components) we can access the button through its **Ref** from inside the price table component.

## The useEffect() Hook

This react Hook is used to manage more complex behavior and changes inside a given component. It works as a “side effect” whenever a component is evaluated, re-evaluated or when a given state changes. The side effect itself is a functions and the effects it analyses are called dependencies. This is the general structure of the useEffect() hook:

```jsx
useEffect(() ⇒ {}, [])
```

The anonymous function is triggered whenever the dependencies - which are states that go inside the square brackets - change. Another useful characteristic of this hook, is that it can be controlled to be triggered in 3 different ways:

1. **No dependency**: the side-effect function will run on **every** state-changes (re-renders);
`useEffect(() ⇒ {})`
2. **Empty array**: the side-effect will run **once**, the first time the component is evaluated (first render);
`useEffect(() ⇒ {}, [])`
3. **Non-empty array**: the side-effect will **whenever there’s a change** on any of the dependencies declared inside the array of dependencies;
`useEffect(() ⇒ {}, [dependency1, dependency2, ..., dependencyN])`

### The useEffect clean-up function

This technique is used in relatively specific scenarios, mostly to optimize http requests. It works with a returned function, that doesn’t run the first time the component is rendered and then runs every time the component is rerendered, before the callback function from useEffect(). See the console logs in the following useEffect example from a form that triggers on every keystroke:

```jsx
useEffect (() => {
    const identifier = setTimeout(()=> {
      console.log('effect')
      setFormIsValid(
        enteredEmail.includes('@') && enteredPassword.trim().length > 6
      );
    }, 500);

    return () => {
      console.log('cleanup')
      clearTimeout(identifier);
    }; //Cleanup function
  }, [enteredEmail, enteredPassword])
```

Console on page render:

```jsx
'effect'
```

Console after first and sub sequential keystrokes:

```jsx
'cleanup'
'effect'
```

In this example, the clean-up function clears the 500ms time out every time a key is pressed, to delay unnecessary HTTP requests. It runs **before** the callback function from useEffect().

## The useReducer() Hook

It is also a state management hook, generally used in more complex situations/components. It allows us to separate the state management logic and rendering logic outside the component. It works in the following way:

![Untitled](React%20-%20The%20complete%20guide%2045b500889b8f495e9449769a94f6159c/Untitled.png)

The reducer function exists outside the component and can receive different dispatches (which are objects) that will trigger different states. All this can happen inside just one reducer function, in contrast to use State, where every state has its own setState function.

**Outside the component:**

```jsx
import React, { useState, useEffect, useReducer } from "react";

const emailReducer = (state, action) => {
  if (action.type === "USER_INPUT") {
    return { value: action.val, isValid: action.val.includes("@") };
  }
  if (action.type === "INPUT_BLUR") {
    return { value: state.value, isValid: state.value.includes("@") };
  }
  return { value: "", isValid: false };
};

const passwordReducer = (state, action) => {
  if (action.type === "USER_INPUT") {
    return { value: action.val, isValid: action.val.trim().length > 6 };
  }
  if (action.type === "INPUT_BLUR") {
    return { value: state.value, isValid: state.value.trim().length > 6 };
  }
  return { value: "", isValid: false };
};
```

**Inside the component:**

```jsx
const Login = (props) => {
  const [formIsValid, setFormIsValid] = useState(false);

  const [emailState, dispatchEmail] = useReducer(emailReducer, {
    value: "",
    isValid: null,
  });

  const [passwordState, dispatchPassword] = useReducer(passwordReducer, {
    value: "",
    isValid: null,
  });

  const {isValid: emailIsValid} = emailState;
  const {isValid: passwordIsValid} = passwordState;

  useEffect(() => {
    const identifier = setTimeout(() => {
      console.log("effect");
      setFormIsValid(emailState.isValid && passwordState.isValid);
    }, 500);

    return () => {
      console.log("cleanup");
      clearTimeout(identifier);
    }; //Cleanup function
  }, [emailIsValid, passwordIsValid]);

  const emailChangeHandler = (event) => {
    dispatchEmail({ type: "USER_INPUT", val: event.target.value });
  };

  const passwordChangeHandler = (event) => {
    dispatchPassword({ type: "USER_INPUT", val: event.target.value });
  };

  const validateEmailHandler = () => {
    dispatchEmail({ type: "INPUT_BLUR" });
  };

  const validatePasswordHandler = () => {
    dispatchPassword({ type: "INPUT_BLUR" });
  };

  return (
    ... // The JSX for the component
  );
};

export default Login;
```

In this scenario, the event handler is dispatching objects to the reducer function, which will apply the validation logic to update a given state. Instead of having 4 different useState() hooks, we can have only one, that will manage everything in a single place, outside the component.

## React Context

To avoid too long chains of props, in order to pass information, we can use the React Context. It essentially stores different states on a global scope, on a separate file. The code contained in that file will also return a JSX component which will be wrapped around the component which will use its states - all the children of that component will also be able to consume directly the context’s states. En example, step by step:

First, we create a context file, using the `createContext()` hook:

```jsx
const MyContext = React.createContext();
 
export default MyContext;
```

Then, inside the App.js, we import the created context and create the desired global variables:

```jsx
import MyContext from './contexts/myContext'
```

```jsx
//declaração dos states
const[nome, setNome] = useState('')
const[email, setEmail] = useState('')
const[idade, setIdade] = useState('')
```

The next step will be to create a **Provider** component, which will contain the states as a value and will wrap our entire application - this enables all child components to directly access all those states:

```jsx
function App(){
 
    const[nome, setNome] = useState('')
    const[email, setEmail] = useState('')
    const[idade, setIdade] = useState('')
 
    return (
        <MyContext.Provider value={{nome, setNome, email, setEmail, idade, setIdade}}>
      //exemplos de possíveis componentes que terão acesso aos states
            <LandingPage/>
            <Menu/>
            <Form/>
            <Register/>
            <Login/>
        </MyContext.Provider>
    )
}
export default App
```

Lastly, in order to use it on the desired child components of App.js, we have to import the created context and destructure the states we wish to use inside the given component:

```jsx
import React, { useContext } from 'react'
import MyContext from '../contexts/myContext'
```

```jsx
const { nome, setNome, email, setEmail, idade, setIdade} = useContext(MyContext)
```

We are now able to get this states and further manipulate them inside our context file.

<aside>
🦉 There’s a lot more to the Context API, including good practices, use cases and patterns.

</aside>

## React under the hood & Optimization Techniques

### React.memo()

Prevents unnecessary re-rendering of components, when wrapped around one. Every time a component is re-evaluated, React renders the component and compares it with the previous render, in order to decide wether it should update the DOM or not. Even though it’s a fast process, on a big scale it can has big impact on performance. `React.memo()` stores the component and reuses it, skipping the next rendering (in case the new props are the same).

```jsx
export function Movie({ title, releaseDate }) {
  return (
    <div>
      <div>Movie title: {title}</div>
      <div>Release date: {releaseDate}</div>
    </div>
  );
}
export const MemoizedMovie = React.memo(Movie);
```

![Untitled](React%20-%20The%20complete%20guide%2045b500889b8f495e9449769a94f6159c/Untitled%201.png)

### useCallback()

This React hook is used to prevent unnecessary re-rendering of functions inside a given component. Through its dependencies one can define in which occasions the functions should be re-evaluated (when the variables used inside the function stay the same, the function will not be re-rendered, just as in `useEffect()`). The function is defined as the first argument of `useCallback()` and the dependencies as the second, inside an array.

```jsx
function ParentComponent() {
    const onHandleClick = useCallback(() => {
        // this will return the same function
        // instance between re-renders
    });

    return (
        <MemoizedSubComponent
            handleClick={onHandleClick}
        />
    );
}
```

<aside>
🦉 Just as with `React.memo()` one should use it with care. `useCallback()` uses memory space and adds at least one line to your code - sometimes making the performance worse.

</aside>

### useMemo()

The same as the last two, but used to prevent unnecessary recalculations of values.

```jsx
const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
```

### When to use React.memo(), useCallback() and useMemo()?

All **three** decide whether to use the previously **cached** content (*value*) or generate a **new** (updated) value (re-render). Using the **cached** version is called **memoization**.

- `memo()`: used for **functional components**
- `useCallback()`: used for **functions**
- `useMemo()`: used for **values**

## Class based components

It’s an alternative functional components. It does not allow us to use hooks, but offers alternatives. It’s good to know it in order to read older codes and older projects.

![Screen Shot 2022-03-08 at 12.12.20.png](React%20-%20The%20complete%20guide%2045b500889b8f495e9449769a94f6159c/Screen_Shot_2022-03-08_at_12.12.20.png)

### State management

Opposed to functional components, states in class based components **always** have to be an object (in functional, it can be numbers, boolean and so on). Example:

```jsx
class Users extends Component {
  constructor() {
    super();
    this.state = {
      showUsers: true,
    };
  }

toggleUsersHandler() {
    this.setState((curState) => {
      return { showUsers: !curState.showUsers };
    });
  }

}
```

in order to update it, we also have to return an object, with the updated information, as showed above.

<aside>
🦉 the `this.state` is initialized inside the constructor and the `this.setState`  can be called anywhere inside the Class. `state` and `setState` words are not arbitrary, they’re built in to React.

</aside>

<aside>
🦉 A Class based component always has to `extends Component` and always need the `super()` constructor in order to be correctly initialized. This happens because, inside React, Component is already a Class that brings built in functionalities.

</aside>

### Side Effects

![Screen Shot 2022-03-08 at 10.17.01.png](React%20-%20The%20complete%20guide%2045b500889b8f495e9449769a94f6159c/Screen_Shot_2022-03-08_at_10.17.01.png)

### Error boundaries

Error boundaries are React’s class based components way of throwing errors. They are not possible to implement on functional based components.

## Sending HTTP ‘GET’ requests

### Handle fetched data with useState()

Just as we store fetched data inside variables in vanilla JS, we can store data in states inside React. The flow is as follows:

1. Initialize a new empty state;
2. Fetch the data using `fetch()`;
3. Create a new variable to store the data;
4. Set the state to this new variable using `setState()`;
5. Use the information inside components as needed;

**An example will be given in the end, explaining all topics of this section.**

### Loading and error statuses

Those informations can also be stores inside statuses. They should be initialized as false and null, respectively. Inside the async/await function, they can be manipulated using `setState()` . We can conditionally render the component based on theses statuses.

### useEffect() and useCallback()

In order to initially fetch data, on page load, we can run the `fetch()` method using the `useEffect()` hook. The `useCallback()` will be used normally, to prevent unnecessary rerendering.

```jsx
import React, { useState, useEffect, useCallback } from 'react';

import MoviesList from './components/MoviesList';
import AddMovie from './components/AddMovie';
import './App.css';

function App() {
  const [movies, setMovies] = useState([]);
  const [isLoading, setIsLoading] = useState(false);
  const [error, setError] = useState(null);

  const fetchMoviesHandler = useCallback(async () => {
    setIsLoading(true);
    setError(null);
    try {
      const response = await fetch('https://swapi.dev/api/films/');
      if (!response.ok) {
        throw new Error('Something went wrong!');
      }

      const data = await response.json();

      const transformedMovies = data.results.map((movieData) => {
        return {
          id: movieData.episode_id,
          title: movieData.title,
          openingText: movieData.opening_crawl,
          releaseDate: movieData.release_date,
        };
      });
      setMovies(transformedMovies);
    } catch (error) {
      setError(error.message);
    }
    setIsLoading(false);
  }, []);

  useEffect(() => {
    fetchMoviesHandler();
  }, [fetchMoviesHandler]);

  function addMovieHandler(movie) {
    console.log(movie);
  }

  let content = <p>Found no movies.</p>;

  if (movies.length > 0) {
    content = <MoviesList movies={movies} />;
  }

  if (error) {
    content = <p>{error}</p>;
  }

  if (isLoading) {
    content = <p>Loading...</p>;
  }

  return (
    <React.Fragment>
      <section>
        <AddMovie onAddMovie={addMovieHandler} />
      </section>
      <section>
        <button onClick={fetchMoviesHandler}>Fetch Movies</button>
      </section>
      <section>{content}</section>
    </React.Fragment>
  );
}

export default App;
```

## Sending HTTP ‘POST’ requests

### Working with Firebase

With Firebase **“Realtime Database”** we are able to create simple JSON APIs both to store (POST) and fetch (GET) data. It is free and easy to use.

An example of a fetch POST:

```jsx
import React, { useState, useEffect, useCallback } from 'react';

import MoviesList from './components/MoviesList';
import AddMovie from './components/AddMovie';
import './App.css';

function App() {
  const [movies, setMovies] = useState([]);
  const [isLoading, setIsLoading] = useState(false);
  const [error, setError] = useState(null);

  const fetchMoviesHandler = useCallback(async () => {
    setIsLoading(true);
    setError(null);
    try {
      const response = await fetch('https://react-http-6b4a6.firebaseio.com/movies.json');
      if (!response.ok) {
        throw new Error('Something went wrong!');
      }

      const data = await response.json();

      const loadedMovies = [];

      for (const key in data) {
        loadedMovies.push({
          id: key,
          title: data[key].title,
          openingText: data[key].openingText,
          releaseDate: data[key].releaseDate,
        });
      }

      setMovies(loadedMovies);
    } catch (error) {
      setError(error.message);
    }
    setIsLoading(false);
  }, []);

  useEffect(() => {
    fetchMoviesHandler();
  }, [fetchMoviesHandler]);

  async function addMovieHandler(movie) {
    const response = await fetch('https://react-http-6b4a6.firebaseio.com/movies.json', {
      method: 'POST',
      body: JSON.stringify(movie),
      headers: {
        'Content-Type': 'application/json'
      }
    });
    const data = await response.json();
    console.log(data);
  }

  let content = <p>Found no movies.</p>;

  if (movies.length > 0) {
    content = <MoviesList movies={movies} />;
  }

  if (error) {
    content = <p>{error}</p>;
  }

  if (isLoading) {
    content = <p>Loading...</p>;
  }

  return (
    <React.Fragment>
      <section>
        <AddMovie onAddMovie={addMovieHandler} />
      </section>
      <section>
        <button onClick={fetchMoviesHandler}>Fetch Movies</button>
      </section>
      <section>{content}</section>
    </React.Fragment>
  );
}

export default App;
```

## Custom hooks

Just as functions in Vanilla JS, React’s custom hooks allows you to extract the logic from a component and make it reusable in other components. All custom hooks **must** start with `use` and it can receive arguments just as a regular JS function. Example:

**Component with logic:**

```jsx
import React, { useState, useEffect } from 'react';

function FriendListItem(props) {
  const [isOnline, setIsOnline] = useState(null);  useEffect(() => {    function handleStatusChange(status) {      setIsOnline(status.isOnline);    }    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);    return () => {      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);    };  });return (
    <li style={{ color: isOnline ? 'green' : 'black' }}>      {props.friend.name}
    </li>);
}
```

**Logic extracted from component:**

```jsx
import { useState, useEffect } from 'react';

function useFriendStatus(friendID) {
  const [isOnline, setIsOnline] = useState(null);

  useEffect(() => {
    function handleStatusChange(status) {
      setIsOnline(status.isOnline);
    }

    ChatAPI.subscribeToFriendStatus(friendID, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(friendID, handleStatusChange);
    };
  });

  return isOnline;
}
```

<aside>
🦉 Just as components, custom hooks must be exported and imported in the files it will be used on.

</aside>

## Forms and user input: good practices

### When to validate?

- On submission
- On focus loss
- On keystroke

Every validation has its up and down-sides. It is usually a good practice to validate each field with the most proper way.

### How to store information from input fields

**setState()**

With the default form events, we can fire `setState()` functions and store the `event.target.value` inside such states.

```jsx
const SimpleInput = (props) => {
  const [enteredName, setEnteredName] = useState('');

  const nameInputChangeHandler = event => {
    setEnteredName(event.target.value);
  }

  return (
    <form>
      <div className='form-control'>
        <label htmlFor='name'>Your Name</label>
        <input type='text' id='name' onChange={nameInputChangeHandler}/>
      </div>
      <div className="form-actions">
        <button>Submit</button>
      </div>
    </form>
  );
};
```

### Validating forms and working with the “was touched” state

A good way to validate a form, is to check if the user input matches our predefined conditions and allow/prevent the form submission based on those conditions. We can also give feedback to the user with that strategy.

```jsx
if (enteredName.trim() === '') {
      setEnteredNameIsValid(false);
      return;
    }
```

In this case, we check if the input field is empty and `return` (stop the submission) if it is empty.

```jsx
{nameInputIsInvalid && (
          <p className='error-text'>Name must not be empty.</p>
        )}
```

We also display an error message, based on the `nameInputIsInvalid` state.

**The “was touched” state**

A common obstacle in this approach is that we shouldn’t start the validation state as true (because it initially isn’t) and shouldn’t show error messages too early (e.g. on page load). To avoid that, we use a second state that checks if the user interacted with a given field.

```jsx
const [enteredNameTouched, setEnteredNameTouched] = useState(false);

const formSubmissionHandler = (event) => {
    event.preventDefault();

    setEnteredNameTouched(true);

    if (enteredName.trim() === '') {
      setEnteredNameIsValid(false);
      return;
    }

    setEnteredNameIsValid(true);

    console.log(enteredName);

    const enteredValue = nameInputRef.current.value;
    console.log(enteredValue);

    // nameInputRef.current.value = ''; => NOT IDEAL, DON'T MANIPULATE THE DOM
    setEnteredName('');
  };
```

We can than further manipulate it, for example, when the form is submitted. To show an error message, both the boolean state that stores the validity **and** the was touched state must be checked.

### Overall Form Validity

With `useEffect()`, we can check the overall form validity every time a given `isFieldValid` state changes:

```jsx
useEffect(() => {
	if (isFieldValid && isField2Valid) {
		setFormIsValid(true);
	} else {
		setFormIsValid(false);
	}
},[isFieldValid, isField2Valid])
```

We can further use the formIsValid state to define conditional css, and control the overall form feedback.

<aside>
🦉 It’s a good practice to build a custom hook to perform the overall form validity. This custom hook checks the validity of the fields after receiving the field specific validation function as an argument.

</aside>

## Redux

### Basic functionality

React Context may present some disadvantages in the following scenarios:

![Screen Shot 2022-04-04 at 16.01.45.png](React%20-%20The%20complete%20guide%2045b500889b8f495e9449769a94f6159c/Screen_Shot_2022-04-04_at_16.01.45.png)

Redux has only one central state storage that receives information from reducer functions and output new states to subscribed components. The basic functionality is as follows:

![Screen Shot 2022-04-04 at 16.07.48.png](React%20-%20The%20complete%20guide%2045b500889b8f495e9449769a94f6159c/Screen_Shot_2022-04-04_at_16.07.48.png)

### First steps

After installing and importing Redux, inside the redux-store.js file, we will have the core elements:

```jsx
import { createStore } from 'redux';

const counterReducer = (state = { counter: 0 }, action) => {
  if (action.type === 'increment') {
    return {
      counter: state.counter + 1,
    };
  }

  if (action.type === 'decrement') {
    return {
      counter: state.counter - 1,
    };
  }

  return state;
};

const store = createStore(counterReducer);

export default store;
```

The `createStore()` function, that creates the central data storage and receives a reducer function, in this case, the `counterReducer` function. The reducer function will have two arguments: the initial state (can be an object or a default fallback value - as used in the example above) and an action. The reducer function will return the new state.

To trigger the reducer functions, we need to dispatch actions. Here are two examples of actions that can be dispatched to the reducer functions above:

```jsx
store.dispatch({ type: 'increment']);
store.dispatch({ type: 'decrement']);
```

Functions or components that use the states provided by Redux are called **subscribers.** To inform Redux which functions and/or components that are using our store we can use the following function: `subscribe()` . An example, following the one above:

```jsx
const counterSubscriber = () => {
	const latestState = store.getState();
	console.log(latestState);
};

store subscribe(counterSubscriber);
```

<aside>
🦉 Redux is not limited to react or to JavaScript, but since we are only using it with react, we will install it like this: `npm install redux react-redux`

</aside>

### Providing the store

Works very similarly to the context API. Components and child components wrapped by the Provider, can access the Redux’s store. We also have to inform where the store is, by importing it and configuring the Provider tag.

```jsx
import { Provider } from '.store;auth-context';
import Store from '.store/index';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
	<Provider store={store}>
		<App />
	</Provider>
);
```

### The useSelector() hook

This hook allows us to retrieve specific states provided by Redux. Inside a given subscriber component, we can call it and give the desired state as an argument:

```jsx
import { useSelector } from 'react-redux';

const Counter = () => {
  const counter = useSelector(state => state.counter);

  const toggleCounterHandler = () => {};

  return (
    <main className={classes.counter}>
      <h1>Redux Counter</h1>
      <div className={classes.value}>{counter}</div>
      <button onClick={toggleCounterHandler}>Toggle Counter</button>
    </main>
  );
};
```

### The useDispatch() hook

To dispatch actions from inside components, we use this hook. Of course, we have to import it on the component’s file, and use it inside the component:

```jsx
import { useDispatch } from 'react-redux';

const Counter = () => {
  const dispatch = useDispatch();
  const counter = useSelector(state => state.counter);

  const incrementHandler = () => {
    dispatch({ type: 'increment' });
  };

  const decrementHandler = () => {
    dispatch({ type: 'decrement' });
  };

  const toggleCounterHandler = () => {};

  return (
    <main className={classes.counter}>
      <h1>Redux Counter</h1>
      <div className={classes.value}>{counter}</div>
      <div>
        <button onClick={incrementHandler}>Increment</button>
        <button onClick={decrementHandler}>Decrement</button>
      </div>
      <button onClick={toggleCounterHandler}>Toggle Counter</button>
    </main>
  );
};

```

In this example, we are using the `<button>` elements to dispatch an action, through its handler functions. The action types are defined inside the dispatch functions, as objects.

**Extra payload to Actions**

If we want to have dynamic reducer functions, we can attach more information to the action’s object and use it inside the reducer functions. For example:

The dispatched action:

```jsx
const increaseHandler = () => {
	dispatch({ type; 'increase', amount: 10})
};

// The reducer function would then, look like this:
if (action.type === 'increment') {
  return {
    counter: state.counter + action.amount,
  };
}
```

<aside>
🦉 **Never** directly manipulate a state, when using redux.

</aside>

### The Redux Toolkit

Solves common problems and simplifies complexities from Redux. Mostly problems derived from the huge complexity of managing various states and reducers.

**The createSlice() hook**

Is a simpler alternative to the reducer functions. There’s no need to return the whole object inside the reducer and you can directly manipulate the state (it doesn’t actually directly manipulate it, it’s just a workaround provided by the toolkit, so the rule is still respected). In the example we’ve been using so far for Redux, a createSlice() would look something like this:

```jsx
const counterSlice = createSlice({
  name: 'counter',
  initialState,
  reducers: {
    increment(state) {
      state.counter++;
    },
    decrement(state) {
      state.counter--;
    },
    increase(state, action) {
      state.counter = state.counter + action.payload;
    },
    toggleCounter(state) {
      state.showCounter = !state.showCounter;
    }
  }
});
```

Note that the initialState is defined outside of the `createSlice()` function and the reducers directly manipulate the state (counter, in this case) and there’s no whole object returned.

**The configureStore() hook**

A friendly abstraction over the standard Redux `createStore` function that adds good defaults to the store setup for a better development experience.

**Dispatching actions with Redux Toolkit**

We first have to define and export the actions inside the store file. In this example:

```jsx
export const counterActions = counterSlice.actions;
```

To dispatch those actions we can just execute the actions defined inside the counterSlice, this way:

```jsx
const incrementHandler = () => {
	dispatch(counterActions.increment());
}

//or

const increaseHandler = () => {
	dispatch(counterActions.increase(10));
}
```

## Advanced Redux

How to use side effects and asynchronous code with Redux. Since in the examples, we are using Firebase just to store information, all the logic has to stay on the Frontend. We are now going to learn where to put our logic, when and where to use useEffect and asynchronous code.

### Where to put our Logic

![Screen Shot 2022-04-12 at 19.33.28.png](React%20-%20The%20complete%20guide%2045b500889b8f495e9449769a94f6159c/Screen_Shot_2022-04-12_at_19.33.28.png)

**Inside the component with sideEffect()**

Firstly, the reducer function will hold the logic that, as already said, happens all on the Frontend. After the logic functions are executed, the component that subscriber to a given state will send a http request to Firebase as a `sideEffect()` . Let’s use a food order app as an example:

Step by step breakdown:

![Screen Shot 2022-04-11 at 19.35.57.png](React%20-%20The%20complete%20guide%2045b500889b8f495e9449769a94f6159c/Screen_Shot_2022-04-11_at_19.35.57.png)

Button (obviously not the complete code):

```jsx
const dispatch = useDispatch();

const { title, quantity, total, price, id } = props.item;

const addItemHandler = () => {
    dispatch(
      cartActions.addItemToCart({
        id,
        title,
        price,
      })
    );
  };

<button onClick={addItemHandler}>+</button>
```

Redux store (also not complete code):

```jsx
import { createSlice } from '@reduxjs/toolkit';

const cartSlice = createSlice({
  name: 'cart',
  initialState: {
    items: [],
    totalQuantity: 0,
  },
  reducers: {
    replaceCart(state, action) {
      state.totalQuantity = action.payload.totalQuantity;
      state.items = action.payload.items;
    },
    addItemToCart(state, action) {
      const newItem = action.payload;
      const existingItem = state.items.find((item) => item.id === newItem.id);
      state.totalQuantity++;
      if (!existingItem) {
        state.items.push({
          id: newItem.id,
          price: newItem.price,
          quantity: 1,
          totalPrice: newItem.price,
          name: newItem.title,
        });
      } else {
        existingItem.quantity++;
        existingItem.totalPrice = existingItem.totalPrice + newItem.price;
      }
    },
  },
});
```

Subscriber component:

```jsx
import { useEffect } from 'react';
import { useSelector } from 'react-redux';

import Cart from './components/Cart/Cart';
import Layout from './components/Layout/Layout';
import Products from './components/Shop/Products';

function App() {
  const showCart = useSelector((state) => state.ui.cartIsVisible);
  const cart = useSelector((state) => state.cart);

  useEffect(() => {
    fetch('https://react-http-6b4a6.firebaseio.com/cart.json', {
      method: 'PUT',
      body: JSON.stringify(cart),
    });
  }, [cart]);

  return (
    <Layout>
      {showCart && <Cart />}
      <Products />
    </Layout>
  );
}

export default App;
```

### Redux DevTools

It’s a Chrome extension that works alongside the Redux Tool Kit. Good for debugging.

## SPA with React Router

Enables the use of different URLs with React. Different routes loads different components.

`$ npm install react-router-dom@5`

### Basic usage

In the App.js file, we can just import Route from react-router-dom and wrap our components with the `<Route path=”/path”>` tag.

In the index.js file, we have to import the BrowserRouter from react-router-dom and wrap our `<App />` with the `<BrowserRouter>` tags.

### Using Links

To prevent the default behaviour of sending http requests every time a link is clicked on a react application, we have to use the `<Link>` element from React Router.

```jsx
<Link to="/welcome">Welcome</Link>
```

The `<NavLink>` component from the Router was created specific for the nav elements ou our application. They basically set a css class when the link is active.

```jsx
<NavLink activeClassName={classes.active} to="/welcome">Welcome</NavLink>
```

### Dynamic Links

The `:` defines that the path is dynamic.

```jsx
<Route path="/product-detail/:productId">
	<ProductDetail />
</Route>
```

With the `useParams()` hook, we can extract a given dynamic parameter from the URL to the component. Example:

```jsx
import { useParams } from 'react-router-dom';

const ProductDetail = () => {
  const params = useParams();

  console.log(params.productId);

  return (
    <section>
      <h1>Product Detail</h1>
      <p>{params.productId}</p>
    </section>
  );
};

export default ProductDetail;
```

React router has its own way of matching URLs. Every path that can be contained inside a given link, matches the link. Check example below, for the products.

### Switch and Exact

<aside>
🦉 Switch doesn’t exist on React Router v6. The Routes component is the substitute.

</aside>

The default URL matching from React Router “your link starts with the defined path”. Example:

```jsx
<Route path='/products'>
		...
</Route>
<Route path='/products/:productId'>
		...
</Route>
```

would both be a match for the path `'/products/:productId'`

The `<Switch>` tag goes around components and change how React Router behaves inside this tag. It will look for the first element that matches the desired path, render it and stop. In the example above, it would stop on the first element.

The `exact` prop is added to a given `<Route>` tag to tell the router that it should be accessed only in case it exactly matches the path. That’s useful for shorter, parent paths.

### The <Prompt> component

This element is used to prevent unwanted navigation. For instance, if an user is filling a form and accidentally tries to go back to the previous page, he can receive a warning.

### The useRouteMatch() function

In order to make more dynamic, flexible route usage, instead of hard coding the path for the URL we are currently at, we can use this function, that stores the current URL in which the user is. Inside a given component, it would look like this:

```jsx
const match = useRouteMatch();
```

And could be used like this:

```jsx
<Route path={`${match.path}/comments`}>
</Route>
```

## Deploying React Apps

### Lazy Loading

Since SPAs will deploy into one big bundled code, it’s better to load only the code that will be visible/used. When we directly import a file inside React, it will be bundled with other files into the final deployed code. Using a React specific function, we can load such file only when the component is rendered.

In order to do that, we have to store that file in a variable with the **same name** of the component. For example, if we have a `<NewQuote>` component, we would create the following variable:

```jsx
const NewQuote = React.lazy(() => import('.pages/NewQuote'));
```

Only doing that, there is a synchronization problem. React needs a fallback UI, that will be showed whilst this file is being downloaded. To do that, we wrap our lazy loaded coded with the `<Suspense fallback={<p>Loading...</p>}></Suspense>` component. Note that the fallback UI is defined as an attribute of such component - and can be another component such as `<LoadingSpinner>`.

### Build the App

The command `npm run build` will create a new folder called ‘build’ which holds all the code to be deployed (moved to the server). The files will be updated automatically every time you run build.

### Uploading the app to a server

SPAa will need only a Static Website Server. Firebase is an example that is free to get started. The first steps of firebase, will be run globally, on the computers terminal. When firebase is initiated, we just have to use the hosting option it gives us.

Also, for SPAs, we have to rewrite all urls to /index.html. Firebase offers this option. 

## User authentication

We are going to authenticate, create, update and delete users using Google’s Firebase Authentication tool. Here’s the [full documentation](https://firebase.google.com/docs/reference/rest/auth?authuser=0#section-create-email-password).

### Adding User Signup

First, we have to enable the user authentication tool on Google Firebase, then select which login methods we are going to use in our application. Firebase has a specific endpoint for each of the available methods (sign up, sign in, logout, change password, delete account, verify email and so on). For signing up, we have first to get the user inputed values (email and password) and send a POST request to Firebase’s specific sign up endpoint. We are going to do this, using the ref attribute inside the form component, and adding a signup handler that will send the request to the API.

```jsx
const submitHandler = (event) => {
    event.preventDefault();

    const enteredEmail = emailInputRef.current.value;
    const enteredPassword = passwordInputRef.current.value;

    // optional: Add validation

    if (isLogin) {
    } else {
      fetch(
        'https://identitytoolkit.googleapis.com/v1/accounts:signUp?key=AIzaSyBZhsabDexE9BhcJbGxnZ4DiRlrCN9xe24',
        {
          method: 'POST',
          body: JSON.stringify({
            email: enteredEmail,
            password: enteredPassword,
            returnSecureToken: true,
          }),
          headers: {
            'Content-Type': 'application/json',
          },
        }
      ).then((res) => {
        if (res.ok) {
          // ...
        } else {
          return res.json().then((data) => {
            // show an error modal
            console.log(data);
          });
        }
      });
    }
```

### User Login

The are only 2 main differences with the sign up process: one is the URL endpoint, and the other is that the login request returns a **Token ID** that can be use globally to ensure that the user is logged in and can access protected/secured data.

### Using the Token as an app-wide state

As this state won’t change very frequently, we can just use React’s Context API instead of Redux. The process goes as follows (just a refresher):

1. Create an auth-context.js file
2. Create a AuthContext const, that stores the token, has a isLogged in variable and two functions: login and logout.
3. Create a AuthContextProvider component that will wrap other components that have access to that data.

```jsx
import React, { useState } from 'react';

const AuthContext = React.createContext({
  token: '',
  isLoggedIn: false,
  login: (token) => {},
  logout: () => {},
});

export const AuthContextProvider = (props) => {
  const [token, setToken] = useState(null);

  const userIsLoggedIn = !!token;

  const loginHandler = (token) => {
    setToken(token);
  };

  const logoutHandler = () => {
    setToken(null);
  };

  const contextValue = {
    token: token,
    isLoggedIn: userIsLoggedIn,
    login: loginHandler,
    logout: logoutHandler,
  };

  return (
    <AuthContext.Provider value={contextValue}>
      {props.children}
    </AuthContext.Provider>
  );
};

export default AuthContext;
```

### User Logout

To log the user out, we just need to clear the token. Check the `logoutHandler` function above. We can access it with the context API.

### Protecting Frontend Pages

In order to protect content from logged out users, we can use React Context’s isLoggedIn state to conditionally render protected Routes:

```jsx
<Layout>
	<Switch>
		<Route path='/' exact>
			<HomePage />
		</Route>
		{authCtx.isLoggedIn && (
			<Route path='/auth'>
				<AuthPage />
			</Route>
		)}
	</Switch>
</Layout>
```

<aside>
🦉 It’s better to also check other ways to do this. The way Max showed in the course doesn’t seem to be secure enough.

</aside>

### Persisting the Login State

Using Firebase’s Token, we can store it on the browser’s local storage. We can do that by using the login/logout handlers:

```jsx
export const AuthContextProvider = (pros) ⇒ {
	{...rest}
	const loginHandler = (token) => {
		setToken(token);
		localStorage.setItem('token', token);
	};
	const logoutHandler = () => {
		setToken(null);
		localStorage.removeItem('token');
	};
}
```

Since the local storage is a synchronous API, we can check if the user is Logged in to set a initial state:

```jsx
export const AuthContextProvider = (pros) ⇒ {
	const initialToken = localStorage.getItem('token');
	const [token, setToken] = useState(initialToken);

{...rest}
};
```

### Auto-logout

The token given by Firebase has a default 1 hour duration. After that, the token is no longer valid and the user must be logged out. To do that, we need to compare the current time with the time given by the token’s expiration. We start with a helper function, outside the AuthContextProvider:

```jsx
const calculateRemainingTime = (expirationTime) => {
	const currentTime = new Date().getTime();
	const adjExpirationTime = new Date(expirationTime).getTime();

	const remainingDuration =  adjExpirationTime - currentTime;

	return remainingDuration;
}
```

Then, inside the loginHandler function, we execute the helper function and use setTimeout to call the logoutHandler function once the time is up:

```jsx
const loginHandler = (token) => {
		setToken(token);
		localStorage.setItem('token', token);

		const remainingTime = calculateRemainingTime(expirationTime);

		setTimeout(logoutHandler, remainingTime);
	};
```

<aside>
🦉 Since the lougoutHandler function is being used as a callback function, it has to de defined **before** the loginHandler function.

</aside>

To get the expirationTime from the login data from Firebase, we can do the following (definitely not the best approach), check the callout:

```jsx
then((data) => {
	const expirationTime = new Date(new Date().getTime() + (+data.expiresIn * 1000));
	authCtx.login(data.idToken, expirationTime.toISOString());
	history.replace('/');
}
```

<aside>
🦉 Max is basically going back and forth, transforming the data to Date, Strings and numbers. Very confusing. The best approach is to directly get the `data.expiresIn`  parse it into a number, and set it to the Timeout.

</aside>
