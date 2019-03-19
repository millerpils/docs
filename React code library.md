# React

## Functional components

Functional components are great for things that don’t really require any concept of dynamic modifications or interaction:

```javascript
    function MyApp() {
        return (
            <ul>
                <li>1</li>
                <li>2</li>
                <li>3</li>
            </ul>
        )
    }

    ReactDOM.render(
        <MyApp />,
        document.getElementById("root")
    )
```

## Class based components

```javascript
    class App extends React.Component {
        constructor() {
            super()
            this.state = {
                isLoggedIn: false
            }  
        }
    
        render() {
            return (
                <div>
                    <h1>You are currently logged {this.state.isLoggedIn ? "in" : "out"}</h1>
                </div>
            )
        }
    }

    export default App
```

## Scope

Each instantiated component receives its own scope. This means we can reuse components as many times as needed without worrying about conflicts.

## Events

```javascript
    <input type="checkbox" checked={props.item.completed} onChange={ () => console.log("Changed!") }/>
```

```javascript
    <input type="checkbox" checked={props.item.completed} onChange={ handleChangeEvent } />

    function handleChangeEvent() {
        console.log('test')
    }
```

## ReactDOM.render

First statement is WHAT we want to render
Second is WHERE do we want to render it

```javascript
    ReactDOM.render(
        <ul>
            <li>1</li>
            <li>2</li>
        </ul>,
        document.getElementById("root")
    )
```

## Styles

Inline styles need to be in a JS object. Things like '-' aren't allowed, e.g background-color. Instead, we use backgroundColor.

A neat way, and a method that would allow of dynamic styles given different values, is to assign a variable:

```javascript
    const styles = {
        fontSize: 30,
        backgroundColor: red
    }

    <h1 style={styles}>Good {timeOfDay}!</h1>
```

## Writing out objects

Using objects as props needs slightly different notation:

```javascript
    <ContactCard 
        contact={{name: "Mr. Whiskerson", imgUrl: "http://placekitten.com/300/200", phone: "(212) 555-1234", email: "mr.whiskaz@catnap.meow"}}
    />
```

We need to go from JS to JSX and to do that we using the double bracket notation - the first gets us into JS, the second gets is into the object. We use the same convention for writing out inline styles.

## Loading data into state

Is as easy as:

```javascript

    import todosData from "./todosData" // json file

    class App extends React.Component {

        constructor() {
            super()
            this.state = {
                todos: todosData
            }
        }

    etc...
```


## setState, prevState and Bind

Whenever we want a class method to be able to modify the state, we need to bind that method to the class.
Below, handClick gets bound.


```javascript
    import React from "react"

    class App extends React.Component {
        constructor() {
            super()
            this.state = {
                count: 0
            }
            this.handleClick = this.handleClick.bind(this)
        }
        
        handleClick() {
            this.setState({ count: 1 })
        }
        
        render() {
            return (
                <div>
                    <h1>{this.state.count}</h1>
                    <button onClick={this.handleClick}>Change!</button>
                </div>
            )
        }
    }

    export default App
```

React has a "built-in" previous state for times where it's useful to know what the previous state is:

```javascript
    handleClick() {
        this.setState(prevState => {
            return {
                count: prevState.count + 1
            }
        })
    }
    
    render() {
        return (
            <div>
                <h1>{this.state.count}</h1>
                <button onClick={this.handleClick}>Change!</button>
            </div>
        )
    }
```

Above we're passing in a function we prevState as an argument than adding one to the count.

## Very simple React app with props and map

### Index.html

```html
    <html>
        <head>
            <link rel="stylesheet" href="style.css">
        </head>
        <body>
            <div id="root"></div>
            <script src="yourjshere.js"></script>
        </body>
    </html>
```

### Index.js

```javascript
    import React from 'react'
    import ReactDOM from 'react-dom'

    import App from "./App"

    ReactDOM.render(<App />, document.getElementById('root'))
```

### App.js

```javascript
    import React from "react"
    import productsData from "./vschoolProducts"
    import Product from "./Product"

    function App() {
        const productsList = productsData.map( product => <Product key={product.id} name={product.name} />) 

        return (
            <div>
            {productsList}
            </div>
        )
    }

    export default App
```

### Product.js

```javascript
    import React from "react"

    function Product(props) {
        return (
            <div>
                {props.name}
            </div>
        )
    }

    export default Product
```

### vschoolProducts Array

```javascript
    const products = [
        {
            id: "1",
            name: "Pencil",
            price: 1,
            description: "Perfect for those who can't remember things! 5/5 Highly recommend."
        },
        {
            id: "2",
            name: "Housing",
            price: 0,
            description: "Housing provided for out-of-state students or those who can't commute"
        },
        {
            id: "3",
            name: "Computer Rental",
            price: 300,
            description: "Don't have a computer? No problem!"
        }
    ]

    export default products
```