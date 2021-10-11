# useFetch

The `useFetch` hook can be used to fetch data across the network.

## The Syntax

```jsx
const { pending, resolved, rejected, data, error } = useFetch(
  url,
  fetchData,
  options
);
```

The `fetchData` function must have the following structure. The first argument receives the url that you pass to `useFetch`, the second argument is the `options` object , and the third argument is an abort controller instance. Below is an example of how your `fetchData` function could look like. You don't need to worry about error handling since the `useFetch` hook handles that for you!

```jsx
const fetchData = (url, params, abortController) => {
  return fetch(url, { ...params, signal: abortController.signal }).then(res => {
    if (!res.ok) new Error(`Error code ${res.status}`);
    return res.json();
  });
};
```

## useFetch arguments

| Argument             | Type       | Explanation                                                                                                                                                                                     |
| -------------------- | ---------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `url`                | `string`   | Location of the resource, like an API URL                                                                                                                                                       |
| `fetchData`          | `function` | Your data fetching function, which receive the `url` and the `opions` object                                                                                                                    |
| `options` (optional) | `object`   | The `options` object will be passed to fetchData function, and should be the second argument that the `fetch ` API accepts. But if it's a simple GET request, then you do not have to pass one. |

## The API

| State      | Type               | Explanation                                                                                                   |
| ---------- | ------------------ | ------------------------------------------------------------------------------------------------------------- |
| `pending`  | `boolean`          | Once the request has started, the pending state will be `true`                                                |
| `resolved` | `boolean`          | Once the request has resolved, then the resolved state will be `true`                                         |
| `rejected` | `boolean`          | If you request was rejected, then the rejected state will be `true`                                           |
| `data`     | `any`              | Represents the data returned from the request.                                                                |
| `error`    | `Error ` or `null` | If the request was rejected, then the error state will point at the Error object and explain what went wrong. |

## Example

[CodeSandbox](https://rrbuc.csb.app/fetch)

```jsx page=src/Fetch.js
import { useState } from "react";

import { useFetch } from "kantan-hooks";

const fetchData = (url, params, abortController) => {
  return fetch(url, { ...params, signal: abortController.signal }).then(res => {
    if (!res.ok) new Error(`Error code ${res.status}`);
    return res.json();
  });
};

const Fetch = () => {
  const { pending, resolved, rejected, data, error } = useFetch(
    `https://jsonplaceholder.typicode.com/comments/`,
    fetchData,
    { method: "GET", headers: { "Content-Type": "application/json" } }
  );
  return (
    <div>
      {pending && "pending..."}
      {rejected && (error.message || "ERROR...")}
      {resolved && <pre>{JSON.stringify(data, null, 2)}</pre>}
    </div>
  );
};
export default Fetch;
```
