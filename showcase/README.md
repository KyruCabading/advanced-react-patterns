# Personal Notes

Writing personal notes here from the The Complete Guide to Advanced React Component Patterns course by Ohans Emmanuel.

## Compound Components Pattern

The Compound Component pattern;

- enables customizability across a group of components
- reduces props overload. Without splitting components into their separate uses, the parent component will need to contain all the props used by its child components.

_Section 4_

## Extending Styles

Allowing components to be styled with custom css is vital for reusable components. Styles are commonly added via the `styles` & `classNames` prop. Allowing styles to be extended can be implemented simply by joining the styles & classNames as a string.

`const classNames = [styles.clap, className].join(" ").trim();`

_Section 5_

## Control Props Patten

The control props pattern enables state to be controlled from some parent component. This is commonly used for inputs or places where multiple components may require the same state. The state and method for updating the state are passed as props to the component(s).

```
<input value={value} onClick={handleClick}/>
```

_Section 6_

## Custom Hooks

Custom hooks allow specific logic to be organized and written in a way that makes them reusable.

_Section 7_

## Props Collections Pattern

The props collections pattern is a way of organizing commonly used props. When numnber of props are commonly used together, it may be worth it to group them into a collection of props. Its usefulness is on a case-by-case basis. There's tradeoffs to consider when deciding whether to group props into a collection.

_Section 8_

## Props Getters Pattern

The props getters pattern is a modification of the props collections pattern which main useful purpose is to allow the user to override or provide their own updates into values within a props collection.

_Section 9_

## State Initializers

State initializers allow the user to set a custom initial state for their usecase. This can be implemented along with a reset state function to bring the current state back to the initialized values.

_Section 10_

### Getting previous state with usePrevious hook.

In this section there's a case where the previous state value of count was used.

```
const usePrevious = (value) => {
  const ref = useRef();

  useEffect(() => {
    ref.current = value;
  }, [value]);

  return ref.current;
};
```

The hook above is an example of how to save the previous value of a given state. How this works is when usePrevious as a hook is first called during the render step of the component it's located in, it creates the initial `ref` with a value of undefined and returns that value as the first value of `usePrevious`. `useEffect` which updates `ref.current = value` is run after as part of the initial mount process and updates `ref.current` to `0`. However this is not returned yet until the next time render is called. When the user clicks clap and increments `count` to 1. `usePrevious` will be re-run on the render phase and return the `ref.current` value which is the correct previous value of 0. Then useEffect will update to store the upcoming previous value of 1.

Note: You might not need access previous props through the usePrevious hook if you just need to **clean up an effect**. Return a cleanup function within `useEffect` for those cases.

```
useEffect(() => {
  ChatAPI.subscribeToSocket(props.userId);
  return () => ChatAPI.unsubscribeFromSocket(props.userId);
}, [props.userId]);
```

In this example, `usePrevious` wasn't necessary, as checking whether running an actual reset is needed through `nonChangingInitialState.current.count !== clapState.count` would have been sufficient.

## State Reducer Pattern

`useReducer` is an alternate way of managing state that uses the same concepts from Redux's method of updating state. The State Reducer pattern can go a step further and allow the user to extend the internal reducer or even call the internal dispatch function themselves.

- Dispatch is an optimized function. No need to pass as a dependency within hooks.

## Choosing the best API

# Useful Links

- beautiful-react-hooks - https://github.com/antonioru/beautiful-react-hooks
