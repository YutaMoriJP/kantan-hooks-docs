# useAbortController

This hook was inspired from this [medium](https://medium.com/doctolib/react-stop-checking-if-your-component-is-mounted-3bb2568a4934) post.

The `useAbortController` hook helps you to abort a fetch request with the `AbortController` API. For example, if the component fetching a resource is unmounted, then it's a good idea to abort the request. For that, simply pass a `signal` property to the fetch API like `fetch(url, {signal: abortController.signal})`.

## The Syntax

```jsx
const abortController = useAbortController(bool);
// your network request
fetch(url, { ...params, signal: abortController.signal });
```

### Argument

| Argument | Type      | Explanation                                                                                               |
| -------- | --------- | --------------------------------------------------------------------------------------------------------- |
| `bool`   | `Boolean` | If you want to instantiate a new `AbortController` instance after a request is aborted, then pass `true`. |

### The API

| State             | Type              | Explanation                                                                                                                                                                                                                                                                                |
| ----------------- | ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `abortController` | `AbortController` | The `useAbortController` hook returns an instance of the AbortController interface. Simply pass the signal property to the fetch API. If you pass the boolean value `true` to the hook, then a new abort controller instance will be instantiated after the previous instance was aborted. |

### Example

By using the `useAbortController` hook, you do not need to handle the native `AbortController` API. Simply pass the abortController.signal to your fetch function and the request will be aborted if necessary. The `useFetch` hook uses the `useAbortController` hook as well.

[CodeSandbox](https://rrbuc.csb.app/abort)

```jsx page=src/AbortController
import { useEffect } from "react";
import { useAbortController } from "kantan-hooks";

const AbortController = () => {
  //if you pass the boolean value true to useAbortController,
  //then a new abort controller instance will be instantiated after the previous abort controller was aborted.
  const abortController = useAbortController(true);
  //redacted for readability
  useEffect(() => {
    const req = async () => {
      await fetch("https://jsonplaceholder.typicode.com/users", {
        //this is IMPORTANT
        signal: abortController.signal,
      });
    };
    req();
  }, []);
  //render fetched data
  return null;
};
```
