# useLocalStorage

The `useLocalStorage` hook helps you to easily manage a React State that will be stored in the LocalStorage API. Check out Example 2 if you are using something like NextJS.

## The Syntax

```jsx
const [state, setState] = useLocalStorage(initialState, localStorageKeyValue);
```

### Arguments

| Argument               | Type     | Explanation                                                                                                                                                                                                                                                                                                                                                                                                                   |
| ---------------------- | -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `initialState`         | `any`    | Pass the state value that you want to manage, like in a normal `useState` hook.                                                                                                                                                                                                                                                                                                                                               |
| `localStorageKeyValue` | `String` | This is different from a `useState` hook, but it's essential for the `useLocalStorage` hook. Pass a unique key value, and it will be used as the key reference for the state stored in the LocalStorage API. You can update it if you want, and the hook will make sure to remove the old item from the LocalStorage API. You have to manage the uniqueness of the key value or else you may end up overwriting stored items. |

### The API

| State      | Type       | Explanation                                                                                            |
| ---------- | ---------- | ------------------------------------------------------------------------------------------------------ |
| `state`    | `any`      | The state value that you pass as the `initialState` argument. If you pass 0, then `state` is 0.        |
| `setState` | `Function` | As the name indicates, the `setState` function is a state setter function that will update your state. |

### Example 1

If you want to keep a reference to the user's preferred theme option, then the `useLocalStorage` hook can be useful.

```jsx page=src/LocalStorage
import { useLocalStorage } from "kantan-hooks";

export default function LocalStorage() {
  const [theme, setTheme] = useLocalStorage("dark", "theme");
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

### Example 2

```jsx page=src/LocalStorage
import { useLocalStorage, useMounted } from "kantan-hooks";

export default function LocalStorage() {
  const [theme, setTheme] = useLocalStorage("dark", "theme");
  const newTheme = theme === "dark" ? "light" : "dark";
  const hasMounted = useMounted();

  //if this code block runs, then your code isn't running client side and does not have access to the LocalStorage API
  if (!hasMounted) return null;

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
