---
sidebar_position: 1
---

# Getting Started

Start your React project with toolchains like [`Create-React-App`](https://create-react-app.dev/), [`NextJS`](https://nextjs.org/docs/), or [`GatsbyJS`](https://www.gatsbyjs.com/docs/tutorial/part-0/). Or use a bundler like [`Parcel`](https://parceljs.org/recipes/react/) and install `react` and `react-dom` yourself. Learn more from the [official docs](https://reactjs.org/docs/create-a-new-react-app.html).

```shell
npx create-react-app my-project && cd my-project
```

## Installation

Once you have your React project started, install the `kantan-hooks` package by running the command:

```shell
npm install kantan-hooks
```

Or do it with yarn:

```shell
yarn add kantan-hooks
```

Next, import the hook that you need. For example, the `useLocalStorage` hook helps you to manage a state that will be stored by the `LocalStorage` API.

```jsx title/App.js
import { useLocalStorage } from "kantan-hooks";

export default function LocalStorage() {
  const [theme, setTheme] = useLocalStorage("dark", "theme");
  const newTheme = theme === "dark" ? "light" : "dark";
  return (
    <div>
      <h1>current theme {theme}</h1>
      <button onClick={() => setTheme(newTheme)}>change Theme</button>
      <button onClick={() => window.location.reload()}>
        Refresh window and check if your state persists!
      </button>
    </div>
  );
}
```
