# useClipboard

The `useClipboard` hook helps you to easily use the copying feature from the [`Clipboard API`](https://developer.mozilla.org/en-US/docs/Web/API/Clipboard_API).

The `useClipboard` hook accepts 2 arguments. The first argument is the value that you want to be copied to the user's clipboard. The second argument is boolean state that should update if the user chooses to copy something to their clipboard, like a code example. Note that the value of the boolean does not matter. It can update from `true` to `false` or vice versa. What matters is that the boolean state is updated, like after clicking a button, `<button>copy</button>`.

```jsx
//The first argument is the value that will be copied to the clipboard
//copied is a boolean state that needs to be updated after a user event occurs
useClipboard("Hello, World", copied);
```

The `useClipboard` hook returns an object with several properties, but you will likely not need them all. The structure of the object looks like `{ idle, pending, resolved, rejected, error }`.

## The Syntax

```jsx
const { idle, pending, resolved, rejected, error } = useClipboard(
  value,
  copied
);
```

### Argument

| Argument | Type      | Explanation                                                 |
| -------- | --------- | ----------------------------------------------------------- |
| `value`  | `string`  | The value that you want to be copied to the clipboard..     |
| `copied` | `boolean` | A boolean that will be toggled when an user action happens. |

### The API

| State      | Type      | Explanation                                                                                 |
| ---------- | --------- | ------------------------------------------------------------------------------------------- |
| `idle`     | `boolean` | The initial state - nothing has happened.                                                   |
| `pending`  | `boolean` | The asynchronous copying operation has started.                                             |
| `resolved` | `boolean` | The asynchronous copying operation has finished, i.e. the value is copied to the Clipboard. |
| `rejected` | `boolean` | The copying operation was rejected for some reason.                                         |
| `error`    | `Error`   | An error object that will contain a message property with what went wrong.                  |

### Example

Although it's not mandatory, you can use the `useToggle` hook to manage the boolean state that is needed for the `useClipboard` hook.
In the example below, the string value "Hello, World" will be copied to the clipboard if the button is clicked. Note the hook ensures that the value is only copied after the user action happens (`copied` is toggled). The value can also be dynamic, like the value from a form element.

```jsx title=src/Clipboard.js
import { useToggle, useClipboard } from "kantan-hooks";
const Clipboard = () => {
  const { open: copied, toggle } = useToggle();
  //"Hello, World" will be copied to the Clipboard
  const { pending, resolved, rejected, error } = useClipboard(
    "Hello, World",
    copied
  );
  return (
    <div>
      <button onClick={toggle}>Copy value to your clipboard</button>
      {pending ? <p>Copying to the clipboard...</p> : null}
      {resolved ? <p>Copied!</p> : null}
      {rejected ? (
        <p role="alert">{error.message || "Something went wrong..."}</p>
      ) : null}
    </div>
  );
};
```

### Optional Third Argument

The `useClipboard` hook also accepts an optional third argument. It's a good idea to let the user know that something was copied to their clipboard. Or letting them know that the copying operation was blocked. For that, create another boolean state with the `useToggle` hook, and pass the `onOpen` function to `useClipboard`.

```jsx
import { useToggle, useClipboard } from 'kantan-hooks';
import { useRef, useEffect } from "react";

const Clipboard = () => {
  //used to manage message state
  const { open, onOpen, onClose } = useToggle(false);
  //used to manage clipboard state
  const { open: copied, toggle } = useToggle();
  const {   resolved, rejected } = useClipboard(
    "HELLO, WORLD",
    copied,
    onOpen
  );
  //used for interval id
  const intervalID = useRef<number>(null!);
  //updates the open state to false
  useEffect(() => {
    intervalID.current = setInterval(onClose, 2000);
    return () => {
      clearInterval(intervalID.current);
    };
  }, [open, onClose]);

  //controls the button text content
  const buttonText =
    open && resolved ? "COPIED" : open && rejected ? "NOT COPIED" : "COPY";

  return <button onClick={toggle}>{buttonText}</button>;
};
```
