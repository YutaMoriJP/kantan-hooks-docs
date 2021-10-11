# useHistory

The `useHistory` hook manages an array of previous state values for you. If you for example want to allow the app user to revert back to an old state, then this hook can come in handy.

## The Syntax

```jsx
//state in sync with the history state
const [historyState, setHistoryState] = useState(null);
//actual current state, that can be updated to the state stored in the history state
const [state, setState] = useState(null);
const { history, filterHistory, clearHistory } = useHistory(historyState);
```

### Argument

| Argument       | Type  | Explanation                                                                                       |
| -------------- | ----- | ------------------------------------------------------------------------------------------------- |
| `historyState` | `any` | Pass a React State that will be updated together with the `state` that you want to keep track of. |

### The API

| State         | Type     | Explanation                                                                                                                                                                                                                                                                                                                          |
| ------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| history       | Array    | An array of all previous state values.                                                                                                                                                                                                                                                                                               |
| filterHistory | Function | A filter function that removes an element from the history state. You must pass an object with an index property like `{index: 1}`, which removes the element at index 1. You can also pass an object with an `id` property like `{id:99}`, but for that, the elements in the history state must be an object with an `id` property. |
| clearHistory  | Function | Clears the history state. Calling the function will update the history state to an empty array.                                                                                                                                                                                                                                      |

### Example

In the code example below, you can create a user profile with attributes like `name` and `age`. When the `onSubmit` event fires, the `user` and `historyState` is updated to an object that can look like `{ name: 'Messi', age: 34, id: 99} `. And as the `historyState` is updated, `history` gets also updated and pushes the newly created user to the `history` array. Let's assume the you have made more than 10 updates. The `history` state then will have 10 user elements. However, if you want to change the `user` state to a profile that you created in your 4th update, then the `history` state can help you out with that. The `revertUser` function receives an old user profile and updates the `user` state to that old profile. See the demo below to make sense of it.

[CodeSandbox](https://rrbuc.csb.app/history)

```jsx page=src/History.js
const History = () => {
  //state in sync with the history state
  const [historyState, setHistoryState] = useState(null);
  //actual current state, that can be updated to the state stored in the history state
  const [user, setUser] = useState(null);
  const { history, filterHistory, clearHistory } = useHistory(historyState);
  const revertUser = oldUser => setUser(oldUser);
  const handleSubmit = newUser => {
    setUser(newUser);
    //this is needed so that when setUser is called, the history state isn't updated
    //it would cause an issue if you for example call the revertUser function
    setHistoryState(newUser);
  };
  return (
    <div>
      {/*Redacted for redability. Think of <Form/> as the component that sets the user -> {name,age,id}*/}
      <Form onSubmit={handleSubmit} />
      <button onClick={clearHistory}>clear history</button>
      {user ? (
        <article>
          <h1>Current User</h1>
          <p>
            name - {user.name} / age - {user.age}
          </p>
        </article>
      ) : null}
      <hr />
      <h2>Past Users</h2>
      {history.length
        ? history.map(pastUser => {
            const { name, age, id } = pastUser;
            return (
              <article key={id}>
                <p>
                  name - {name} / age - {age}
                </p>
                <button onClick={() => filterHistory({ id })}>
                  Remove user
                </button>
                <button onClick={() => revertUser(pastUser)}>
                  Go back to this user
                </button>
              </article>
            );
          })
        : null}
    </div>
  );
};
```
