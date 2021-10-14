# useHeight

The `useHeight` hook returns the height of the ref that you pass to the hook.

## The Syntax

```jsx
const divRef = useRef(null);
const height = useHeight(ref); //or useHeight({ current: window })
return <div ref={divRef} />;
```

### Argument

| Argument | Type                         | Explanation                                                                                                                                                                                                                                                                                                                                                                                     |
| -------- | ---------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `ref`    | `ref` or `{current: window}` | The ref that you pass to `useHeight` must have a reference to a DOM node, which can be achieved by calling the `useRef` hook and passing the ref object like this `<div ref={ref} />`. You also have the option to pass an object with a `current` property that points at `window`, like `{current: window}`. If you pass the `window` object, then you will get the `height` of the viewport. |

### The API

| State    | Type     | Explanation                                                                                                                              |
| -------- | -------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| `height` | `Number` | It returns the `height` value of the DOM node that the `ref` object points at, or the `viewport height` if you pass the `window` object. |

### Example

[CodeSandbox](https://rrbuc.csb.app/height)

```jsx title=src/Counter.js
import { useHeight } from "kantan-hooks";
import { useRef } from "react";

const Height = () => {
  const divRef = useRef(null);
  const divHeight = useHeight(divRef);
  const windowHeight = useHeight({ current: window });

  return (
    <div ref={divRef} style={{ border: "2px solid black" }}>
      <h1>Hello, useHeight</h1>
      {/*in the initial render, height points at null, but after useLayoutEffect runs, it will point at a number*/}
      {divRef.current ? (
        <section>
          <p>The div height is {divHeight}</p>
          <p>The window height is {windowHeight}</p>
        </section>
      ) : null}
    </div>
  );
};
export default Height;
```
