# useMediaQuery

The `useMediaQuery` can come in handy if you want to display a different UI, depending on the user's viewport, like mobile and desktop.

The `useMediaQuery` hook returns a boolean value if the media query string that you pass to the hook matches with the user's viewport. For example, if you call `useMediaQuery("(max-width: 500px)")` and the user's viewport is smaller than `500px`, then the hook return the boolean value `true`.

```jsx
const App = () => {
  const isMobile = useMediaQuery("(max-width: 500px)");
  const isTablet = useMediaQuery("(min-width:500px) and (max-width:900px)");
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
