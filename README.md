# nonstated
simple react state management library (inspired by unstated)

[![npm](https://img.shields.io/npm/v/nonstated.svg?style=flat-square)](https://www.npmjs.com/package/nonstated)

## Install
```
yarn add nonstated
```

### Usage
```jsx
import {Container} from 'nonstated'

class CounterContainer extends Container{
    state = {value: 0}
    increment() {
        this.setState({value: this.state.value + 1})
    }
    decrement() {
        this.setState({value: this.state.value - 1})
    }
}

const counter = new CounterContainer()

function Counter () {
    return (
        <div>
            <span>{counter.on(state => state.value)}</span>
            <button onClick={() => counter.decrement()}> - </button>
            <button onClick={() => counter.increment()}> + </button>
        </div>)
}
```

## API
### container.on()
Dynamically subscribe container state within a render.
```jsx
function Counter () {
    return (
        <div>
            <span>{counter.on(state => state.value)}</span>
            <button onClick={() => counter.decrement()}> - </button>
            <button onClick={() => counter.increment()}> + </button>
        </div>)
}
```

### subscribe(containers [, selector])
HOC is also possible.
```jsx
import {subscribe} from 'nonstated'

subscribe(counter)(function({ state }) {
    return <span>{state.value}</span>
})
```

#### selector
selector results are passed to the props.
```jsx
const selector = state => state.value

subscribe(counter, selector)(function({ state: value }) {
    return <span>{value}</span>
})
```

#### Subscribe to multiple containers
This is possible using arrays.
```js
subscribe([counter, form])(function({ state: [counterState, formState] }) {
    // ...
})
```

### subscribeOnly
Wrap with `React.PureComponent`. Unnecessary render execution is reduced, but does not respond to parent subscriptions.
```js
import {subscribeOnly} from 'nonstated'

subscribeOnly(counter)(function({ state }){
    // ...
})
```


## License
MIT
