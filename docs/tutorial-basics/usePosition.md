# usePosition

The `usePosition` hook returns an `object` with data representing the space around the DOM node. For example, if the space above a DOM node is 100px, space below the DOM node is 150px, space left to the DOM node is 200px, and space right to the DOM node is 250px, then the hook returns the following object `{ top: 100, right: 250, bottom: 150, left: 200 }`. Whenever you want to know how much space is available around a DOM node, then the `usePosition` hook will help you.

## The Syntax

```jsx
const ref = useRef(null);
const position = usePosition(ref);
```

### Argument

| Argument | Type     | Explanation                                                                                  |
| -------- | -------- | -------------------------------------------------------------------------------------------- |
| `ref`    | `Object` | Pass a ref that has a reference to a DOM node, which can be done like this `<div ref={ref}>` |

### The API

| State      | Type     | Explanation                                                                                                                                                                                                                                                                                           |
| ---------- | -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `position` | `Object` | In the initial render when the `ref` is still not set, the hook returns an empty object `{}`. After the `ref` is set to a DOM node, the hook returns an object with the following structure `{top:10, right:10, bottom:10, left:10}`. The properties represent the space around the DOM node in `px`. |

### Example

[CodeSandbox](https://rrbuc.csb.app/position)

```jsx
import { usePosition } from "kantan-hooks";

const App = () => {
  const divRef = useRef(null);
  //you could destruct {top, right, bottom, left} but note that in the initial render, they will all be undefined
  const position = usePosition(divRef);
  return (
    <>
      <div ref={position}>
        <h1>Hello, usePosition</h1>
      </div>
      {position ? (
        <ul>
          <li>top {position.top}</li>
          <li>right {position.right}</li>
          <li>bottom {position.bottom}</li>
          <li>left {position.left}</li>
        </ul>
      ) : null}
    </>
  );
};
```
