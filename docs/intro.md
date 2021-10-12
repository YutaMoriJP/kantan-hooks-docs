---
sidebar_position: 1
---

# Getting Started

Start your React project with toolchains like [`Create-React-App`](https://create-react-app.dev/), [`NextJS`](https://nextjs.org/docs/), or [`GatsbyJS`](https://www.gatsbyjs.com/docs/tutorial/part-0/). Or use a bundler like [`Parcel`](https://parceljs.org/recipes/react/) and install `react` and `react-dom` yourself. Learn more from the [official docs](https://reactjs.org/docs/create-a-new-react-app.html).

```shell
npx create-react-app my-project && cd my-project
```

## Installation

Once you have your React project started, install the `kantan-hooks` package by using the command:

```shell
npm install kantan-hooks
```

Or do it with yarn:

```shell
yarn add kantan-hooks
```

Next, import the hook you need for your component, like the `useToggle` hook to easily manage a boolean state. It returns an object with 4 properties, `open`, `onOpen`, `onClose`, and `toggle`. `open` is a boolean React state, so it's either `true` or `false`. And `onOpen` (updates open to true), `onClose` (updates open to false), and `toggle`(toggles the open state) are the update functions, that will update the `open` state. Play around in [CodeSandbox](https://rrbuc.csb.app/toggle), and try out different things like conditionally rendering a React Component, etc.

The `useToggle` hook will come in handy in all kinds of situations. Later you will encounter the `useClipboard` hook that simplifies the Clipboard API for you, and the `useToggle` hook will help you out.

### The Syntax

```jsx
const { open, onOpen, onClose, toggle } = useToggle(initial);
```

### Argument

| Argument  | Type      | Explanation                                    |
| --------- | --------- | ---------------------------------------------- |
| `initial` | `Boolean` | The initial boolean value of the `open` state. |

### The API

| State     | Type       | Explanation                                                                                 |
| --------- | ---------- | ------------------------------------------------------------------------------------------- |
| `open`    | `Boolean`  | A boolen state that will be updated when the state setter functions are called.             |
| `onOpen`  | `Function` | A state setter function that updates the `open` state to `true`                             |
| `onClose` | `Function` | A state setter function that updates the `open` state to `false`                            |
| `toggle`  | `Function` | A state setter function that toggles the `open` state from `true` to `false` or vice versa. |

### Example

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
