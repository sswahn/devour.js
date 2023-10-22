# Bind
Bind is a lightweight JavaScript framework designed for managing state and connecting components to state changes.

## Overview
The framework provides core utilities to:

  · Create a centralized state store  
  · Dispatch actions to update the state  
  · Bind components to state changes and auto-update them  
  · Render DOM elements and components  
  · Event delegation

## Documentation  
### Import
```javascript
import {createStore, bind, html, onUpdate} from '@sswahn/bind'
```  

### Create State  
Used to create a new store with the given initial state.  
```javascript
createStore({
  count: 0,
  user: null
})
```  

### Get State  
Bound components have access to the context parameter. It provides a copy of the current bound state.  
```javascript
context.count
```  

### Update State  
Bound components have access to the dispatch parameter. It dispatches an action to the store.  
```javascript
dispatch({ type: 'count', payload: 1 })
```  

### Bind State  
Binds a component to a specific state change.  
```javascript
const BoundComponent = bind('count', MyComponent)
```  

### onUpdate Hook  
A lifecycle hook to perform operations after a component is rendered.  
```javascript
const element = html('div')
onUpdate(element, () => {
  console.log('Fires post render.')
})
```  

 ### Create An HTML Element  
A utility function to create DOM elements and event delegation.

Parameters:  
  · **type**: The type of DOM element to create (e.g., "div", "span").  
  · **attributes**: An object of attributes to apply to the DOM element.  
  · **children**: An array of child nodes or text to append to the created element.  
```javascript
const myDiv = html('div', { class: 'my-class', textContent: 'Hello!' }, [
  html('span', {}, ['Child span'])
])
```  

## Example
```javascript
// index.js
import { createStore } from '@sswahn/bind'
import Counter from './Counter'

createStore({ counter: 0 })
document.getElementById('root').appendChild(Counter())
```
```javascript
// Counter.js
import { html } from '@sswahn/bind'
import Button from './Button'
import Display from './Display'

const Counter = () => {
  const attributes = {
    id: 'counter',
    class: 'section'
  }
  const children = [
    Button()
    Display()
  ]
  return html('div', attributes, children)
}

export default Counter
```
```javascript
// Button.js
import { html, bind } from '@sswahn/bind'

const Button = ({ context, dispatch }) => {
  const increment = event => {
    dispatch({
      type: 'counter',
      payload: context.counter + 1
    })
  }
  return html('button', {
    onClick: increment,
    textContent: '+'
  })
}

export default bind('counter', Button)
```
```javascript
// Display.js
import { html, bind } from '@sswahn/bind'

const Display = ({ context }) => {
  return html('span', {
    textContent: context.counter
  })
}

export default bind('counter', Display)
```

## License
Bind is [MIT Licensed](https://github.com/sswahn/bind/blob/main/LICENSE)
