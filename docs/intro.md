---
sidebar_position: 1
---

# Getting Started

Start your React project with toolchains like [`Create-React-App`](https://create-react-app.dev/), [`NextJS`](https://nextjs.org/docs/), or [`GatsbyJS`](https://www.gatsbyjs.com/docs/tutorial/part-0/). Or use a bundler like [`Parcel`](https://parceljs.org/recipes/react/) and install `react` and `react-dom` yourself. Learn more from the [official docs](https://reactjs.org/docs/create-a-new-react-app.html).

## Installation

Once you have your React project started, install the `kantan-hooks` package by using the command:

```shell
npm install kantan-hooks
```

Or do it with yarn:

```shell
yarn add kantan-hooks
```

Next, import the hook you need for your component, like the `useToggle` hook to easily manage a toggle state. It returns an object with 4 properties, `open`, `onOpen`, `onClose`, and `toggle`. `open` is a boolean React state, so it's either `true` or `false`. And `onOpen` (updates open to true), `onClose` (updates open to false), and `toggle`(toggles the open state) are the update functions, that will update the `open` state. Play around in [CodeSandbox](https://codesandbox.io/s/small-sea-rrbuc?file=/src/Toggle.tsx), and try out different things like conditionally rendering a React Component, etc.

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
