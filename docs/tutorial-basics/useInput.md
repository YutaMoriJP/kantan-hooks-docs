# useInput

In React, form elements like `input` and `textarea` are usually managed by React. A form element managed by React is called a `Controlled Component`. Creating a React State like `const [value, setValue] = React.useState('')` can become very repetetive. Let's use a custom hook to simplify the task for us!

The `useInput` hook returns an array with 2 elements. The first element is an object that has the following structure `{ value, onChange }` and it will manage the Form element's state for you. The second element is a function that will reset the input value to the initial value. So, if you passed an empty string to `useInput`, then the value will be updated to an empty string.

## The Syntax

```jsx
const [inputFields, resetState] = useInput("");
```

### The API

| State                 | Type     | Explanation                                                                                                                                                                                                                                                          |
| --------------------- | -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `{ value, onChange }` | Object   | The `{ value, onChange }` object is passed directly to the Form element, and it will manage the state. You can use the [`spread syntax`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax), like `<input {...inputFields}>` |
| `resetState`          | Function | A helper function that will update the value state to the initial state passed to the hook                                                                                                                                                                           |

### Example

[CodeSandbox](https://rrbuc.csb.app/input)

```jsx title="src/Input.js"
import { useInput } from "kantan-hooks";

export default function Input() {
  //destruct the array
  const [nameFields, resetName] = useInput("");
  const [ageFields, resetAge] = useInput("");
  //destruct the nameFields/ageFields object inside the <input/> element like
  //<input {...nameFields}/>

  //if you have multiple form elements, then create a reset function
  const handleReset = () => {
    resetName();
    resetAge();
  };
  return (
    <>
      <label htmlFor="username">
        Username
        <input
          type="text"
          id="username"
          placeholder="Your name..."
          aria-label="Your username"
          {...nameFields}
        />
      </label>
      <label htmlFor="age">
        Age
        <input
          type="number"
          id="age"
          placeholder="Your age..."
          aria-label="Your age"
          {...ageFields}
        />
      </label>
      <button onClick={handleReset}>Clear Form</button>
    </>
  );
}
```

## Constraints

Sometimes you want to constraint what the user types into the form element. For that, you can pass an options object with a `handleChange` function. The `handleChange` function receives 2 arguments. The first argument is the new input field value, and the second argument is the current input field state, like `handleChange(newState, previousState)`. Let's say your form element only allows uppercase characters. Write a function like below.

```jsx
const handleChange = (value: string) => {
  //if the value is "a" then "A" is returned
  return value.toUpperCase();
};
const [upperCaseFields] = useInput("", { handleChange });
```
