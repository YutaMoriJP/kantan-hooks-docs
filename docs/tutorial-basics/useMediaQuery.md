# useMediaQuery

The `useMediaQuery` can come in handy if you want to display a different UI, depending on the user's viewport, like mobile and desktop.

The `useMediaQuery` hook returns the boolean value `true` if the media query string that you pass to the hook matches with the user's viewport. For example, if you call `useMediaQuery("(max-width: 500px)")` and the user's viewport is smaller than `500px`, then the hook return the value`true`. If your React app uses client side rendering, then that's all you need. However, if you use a framework like NextJS that runs your code first server side, then you might want to take advantage of the `useMounted` hook. Check out Example 2.

## The Syntax

```jsx
const matches = useMediaQuery(mediaQueryString);
```

### Argument

| Argument           | Type     | Explanation                                                                                                             |
| ------------------ | -------- | ----------------------------------------------------------------------------------------------------------------------- |
| `mediaQueryString` | `String` | Pass a media query like `(max-width: 450px)` if you want to know whether the user's device width is smaller than 450px. |

### The API

| State     | Type      | Explanation                                                                                                                   |
| --------- | --------- | ----------------------------------------------------------------------------------------------------------------------------- |
| `matches` | `Boolean` | If the given query string matches with the user's viewport, the returned state value is true. If not then `false` is returned |

### Example 1

[CodeSandbox](https://rrbuc.csb.app/mediaquery)

```jsx
import { useMediaQuery } from "kantan-hooks";
const App = () => {
  const isMobile = useMediaQuery("(max-width: 500px)");
  const isTablet = useMediaQuery("(min-width:500px) and (max-width:900px)");
  //client side apps don't need to worry about this. But if your app uses server side rendering, then this checker is necessary.
  if (isMobile)
    return (
      <div>
        <h1>The viewport is pretty small</h1>
        <p>
          It might be a good idea to render a mobile specific navbar or
          something.
        </p>
      </div>
    );
  //redacted for readability
  if (isTablet) return null;
  return null;
};
```

### Example 2

This Example is useful for apps using frameworks like NextJS, GatsbyJS, or any app that is rendered server side.
[CodeSandbox](https://rrbuc.csb.app/mediaquery)

```jsx
import { useMediaQuery, useMounted } from "kantan-hooks";
const App = () => {
  const isMobile = useMediaQuery("(max-width: 500px)");
  //if hasMounted is true, then you know that the component has mounted, and you can use the numerous Web APIs
  const hasMounted = useMounted();
  if (!hasMounted) return null;
  if (isMobile)
    return (
      <div>
        <h1>The viewport is pretty small</h1>
        <p>
          It might be a good idea to render a mobile specific navbar or
          something.
        </p>
      </div>
    );
  //redacted for readability
  return (
    <div>
      <h1>Use a Desktop UI</h1>
    </div>
  );
};
```
