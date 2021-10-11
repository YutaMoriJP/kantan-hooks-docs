# useLocalStorage

The `useLocalStorage` hook helps you to easily manage a React State that will be stored in the LocalStorage API.

## The Syntax

```jsx
const [state, setState] = useLocalStorage(initialState, localStorageKeyValue);
```

## useLocalStorage Arguments

| Argument               | Type     | Explanation                                                                                                                                                                                                                                                                                                               |
| ---------------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `initialState`         | `any`    | Pass the state value that you want to manage, like in a normal `useState` hook.                                                                                                                                                                                                                                           |
| `localStorageKeyValue` | `string` | This is different from a `useState` hook, but it's essential for the `useLocalStorage` hook. Pass an unique key value, and it will be used as the key reference for the state stored in the LocalStorage API. You can update it if you want, and the hook will make sure to remove the old item from the LocalStorage API |

## The API

| State      | Type       | Explanation                                                                                            |
| ---------- | ---------- | ------------------------------------------------------------------------------------------------------ |
| `state`    | `any`      | The state value that you pass as the `initialState` argument. If you pass 0, then `state` is 0.        |
| `setState` | `Function` | As the name indicates, the `setState` function is a state setter function that will update your state. |

## Example

If you want to keep a reference to the user's preferred theme option, then the `useLocalStorage` hook can be useful.

```jsx page=src/LocalStorage
import { useLocalStorage } from "kantan-hooks";

export default function LocalStorage() {
  const [theme, setTheme] = useLocalStorage("theme", "dark");
  const newTheme = theme === "dark" ? "light" : "dark";
  return (
    <div>
      <h1>current theme {theme}</h1>
      <button onClick={() => setTheme(newTheme)}>Change Theme</button>
      <button onClick={() => window.location.reload()}>
        Refresh window and check if your state persists
      </button>
    </div>
  );
}
```
