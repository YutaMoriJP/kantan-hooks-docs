# useToggle

Next, import the hook you need for your component, like the `useToggle` hook to easily manage a toggle state. It returns an object with 4 properties, `open`, `onOpen`, `onClose`, and `toggle`. `open` is a boolean React state, so it's either `true` or `false`. And `onOpen` (updates open to true), `onClose` (updates open to false), and `toggle`(toggles the open state) are the update functions, that will update the `open` state. Play around in [CodeSandbox](https://codesandbox.io/s/small-sea-rrbuc?file=/src/Toggle.tsx), and try out different things like conditionally rendering a React Component, etc.

The `useToggle` hook will come in handy in all kinds of situations. Later you will encounter the `useClipboard` hook that simplifies the Clipboard API for you, and the `useToggle` hook will help you out.

### The Syntax

```jsx
const { open, onOpen, onClose, toggle } = useToggle(initial);
```

### The API

| State     | Type     | Explanation                                                                                 |
| --------- | -------- | ------------------------------------------------------------------------------------------- |
| `open`    | Boolean  | A boolen state that will be updated when the state setter functions are called.             |
| `onOpen`  | Function | A state setter function that updates the `open` state to `true`                             |
| `onClose` | Function | A state setter function that updates the `open` state to `false`                            |
| `toggle`  | Function | A state setter function that toggles the `open` state from `true` to `false` or vice versa. |

### Example

[CodeSandbox](https://rrbuc.csb.app/toggle)

```jsx title="src/App.js"
import { useToggle } from "kantan-hooks";

export default function App() {
  //destruct the object returned by useToggle
  const { open, onOpen, onClose, toggle } = useToggle(false);
  return (
    <>
      <h1>Turn the Switch on/off</h1>
      <button onClick={toggle}>Toggle Switch</button>
      <button onClick={onOpen} disabled={open}>
        Turn on
      </button>
      <button onClick={onClose} disabled={!open}>
        Turn off
      </button>
    </>
  );
}
```
