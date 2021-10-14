# useWidth

The `useWidth` hook returns the width of the ref that you pass to the hook.

## The Syntax

```jsx
const divRef = useRef(null);
const width = useWidth(ref); //or useWidth({ current: window })
return <div ref={divRef} />;
```

### Argument

| Argument | Type                         | Explanation                                                                                                                                                                                                                                                                                                                                                                                   |
| -------- | ---------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `ref`    | `ref` or `{current: window}` | The ref that you pass to `useWidth` must have a reference to a DOM node, which can be achieved by calling the `useRef` hook and passing the ref object like this `<div ref={ref} />`. You also have the option to pass an object with a `current` property that points at `window`, like `{current: window}`. If you pass the `window` object, then you will get the `width` of the viewport. |

### The API

| State   | Type     | Explanation                                                                                                                            |
| ------- | -------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| `width` | `Number` | It returns the `width` value of the DOM node that the `ref` object points at, or the `viewport width` if you pass the `window` object. |

### Example

[CodeSandbox](https://rrbuc.csb.app/width)

```jsx title=src/Width.js
import { useWidth } from "kantan-hooks";
import { useRef } from "react";

const Width = () => {
  const divRef = useRef(null);
  const divWidth = useWidth(divRef);
  const windowWidth = useWidth({ current: window });
  return (
    <div ref={divRef} style={{ border: "2px solid black" }}>
      <h1>Hello, useWidth</h1>
      {/*in the initial render, Width points at null, but after useLayoutEffect runs, it will point at a number*/}
      {divRef.current ? (
        <section>
          <p>The div Width is {divWidth}</p>
          <p>The window Width is {windowWidth}</p>
        </section>
      ) : null}
    </div>
  );
};
export default Width;
```
