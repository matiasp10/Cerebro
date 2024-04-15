```
React.startTransition(callback)
```

`React.startTransition` lets you mark updates inside the provided callback as transitions. This method is designed to be used when [`React.useTransition`](https://es.reactjs.org/docs/hooks-reference.html#usetransition) is not available.

> Note:
> 
> Updates in a transition yield to more urgent updates such as clicks.
> 
> Updates in a transition will not show a fallback for re-suspended content, allowing the user to continue interacting while rendering the update.
> 
> `React.startTransition` does not provide an `isPending` flag. To track the pending status of a transition see [`React.useTransition`](https://es.reactjs.org/docs/hooks-reference.html#usetransition).