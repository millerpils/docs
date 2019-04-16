# Redux

## createStore

Allows us to create a store that holds all of our data

## Provider

Wraps the App component and allows us to pass the store by way of props

## Actions

The only way to change the state is to emit an action; an object describing what
happened

## Reducers

Reducers specify how the state tree is transformed by actions

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