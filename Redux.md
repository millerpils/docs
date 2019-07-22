# Redux

## createStore

Allows us to create a store that holds all of our data

## Provider

Wraps the App component and allows us to pass the store by way of props

## Actions

Actions are payloads of information that send data from your application to your store. They are the only source of information for the store. You send them to the store using store.dispatch().

## Action Creators

Action creators are exactly that—functions that create actions. 

```javascript
  function addTodo(text) {
    return {
      type: ADD_TODO,
      text
    }
  }
```

## Reducers

Reducers specify how the application's state changes in response to actions sent to the store. Remember that actions only describe what happened, but don't describe how the application's state changes. The reducer is a pure function that takes the previous state and an action, and returns the next state.

### cartReducer function

This function takes two parameters: the state and action

## mapStateToProps

Takes the state in our cartReducer and passes it as props to the file

```javascript
const mapStateToProps = state => {
  return {
    items: state.items
  }
}
```