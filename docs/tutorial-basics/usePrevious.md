# usePrevious

The `usePrevious` hook helps you to keep a reference of the previous state value.

## The Syntax

```jsx
const previous = usePrevious(state);
```

## The API

| State      | Type | Explanation                                                                                 |
| ---------- | ---- | ------------------------------------------------------------------------------------------- |
| `previous` | any  | If the state passed to `usePrevious` was updated from 4 to 5, then the previous value is 4. |

## Example

```jsx title=src/Counter.js
import { usePrevious } from "kantan-hooks";

const Counter = () => {
  const [count, setCount] = useState(0);
  //basic previous usage
  const previous = usePrevious(count);
  return (
    <>
      <h1>
        Current {count} / previous {previous}
      </h1>
      <button onClick={() => setCount(c => c + 1)}>+</button>
    </>
  );
};
```
