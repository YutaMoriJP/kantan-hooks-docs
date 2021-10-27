# useMediaQuery

The `useMediaQuery` can come in handy if you want to display a different UI, depending on the user's viewport, like mobile and desktop.

The `useMediaQuery` hook returns an array of boolean values if the media query string that you pass to the hook matches with the user's viewport. For example, if you call `useMediaQuery("(max-width: 500px)")` and the user's viewport is smaller than `500px`, then the hook return an array with the first element's value being `true`. If your React app uses client side rendering, then that's all you need. However, if you use a framework like NextJS that runs your code first server side, then you need to make use of the second element. The second value is a `boolean` state that tells you that the hook finished matching the media query with the viewport. This is necessary since the hook uses the `window` object under the hood, but that only exists in the browser, and is `undefined` server-side.

## The Syntax

```jsx
const [matches, resolved] = useMediaQuery(mediaQueryString);
```

### Argument

| Argument           | Type     | Explanation                                                                                                             |
| ------------------ | -------- | ----------------------------------------------------------------------------------------------------------------------- |
| `mediaQueryString` | `String` | Pass a media query like `(max-width: 450px)` if you want to know whether the user's device width is smaller than 450px. |

### The API

| State      | Type      | Explanation                                                                                                                                              |
| ---------- | --------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `matches`  | `Boolean` | If the given query string matches with the user's viewport, the returned state value is true. If not then `false` is returned                            |
| `resolved` | `Boolean` | If `false`, then the hook has not matched the media query to the viewport yet. This is necessary for apps that use server side rendering. See Example 2. |

This reading[https://www.joshwcomeau.com/react/the-perils-of-rehydration/] might be useful to understand why the `resolved` value is necessary for apps that use Frameworks like Gatsby or Next.

### Example 1

[CodeSandbox](https://rrbuc.csb.app/mediaquery)

```jsx
import { useMediaQuery } from "kantan-hooks";
const App = () => {
  const [isMobile, mobileResolved] = useMediaQuery("(max-width: 500px)");
  const [isTablet, tabletResolved] = useMediaQuery(
    "(min-width:500px) and (max-width:900px)"
  );
  //client side apps don't need to worry about this. But if your app uses server side rendering, then this checker is necessary.
  if (!mobileResolved) return null;
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

[CodeSandbox](https://rrbuc.csb.app/mediaquery)

```jsx
import { useMediaQuery } from "kantan-hooks";
const App = () => {
  const [isMobile, resolved] = useMediaQuery("(max-width: 500px)");
  //this could also be a Loading animation
  if (!resolved) return null;
  //if this block executes, then the media query has been matched to the viewport
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
