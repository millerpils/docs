# React

## Functional components

Functional components are great for things that don’t really require any concept of dynamic 
modifications or interaction:

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

Whenever we want to use state, we need classes

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

##Lifecycle methods

These methods are available for use throughout the lifecycle of an application.

### componentDidMount

componentDidMount() is a method hook that can be run some kind of code immediately after the component first mounts to the DOM. A common use is to get data from somewhere so the component can do what it's supposed to do.

```javascript
    class App extends Component {
        constructor() {
            super()
            this.state = {
                character: {}
            }
        }
        
        componentDidMount() {
            fetch("https://swapi.co/api/people/1")
                .then(response => response.json())
                .then(data => {
                    this.setState({
                        character: data
                    })
                })
        }
        
        render() {
            return (
                <div>
                    {this.state.character.name}
                </div>
            )
        }
    }

    export default App
```

## Scope

Each instantiated component receives its own scope. This means we can reuse components as 
many times as needed without worrying about conflicts.

## Events

Events can occur using onChange, onClick etc. We can use an arrow function direct or call a function:

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

Inline styles need to be in a JS object. Things like '-' aren't allowed, e.g background-color. 
Instead, we use backgroundColor.

A neat way, and a method that would allow of dynamic styles given different values, is to assign a variable:

```javascript
    const styles = {
        fontSize: 30,
        backgroundColor: red
    }

    <h1 style={styles}>Good {timeOfDay}!</h1>
```

## Conditional rendering

### &&

Traditionally, the and operator would consider both the left and right parts of the statement, if this and that are true, then the statement is true. The && operator in React is different - if the thing on the left is true, it immediately returns the thing on the right.

```javascript
    this.state.unreadMessages.length > 0 && 
    <h2>You have {this.state.unreadMessages.length} unread messages!</h2>
```

## Writing out objects

Using objects as props needs slightly different notation:

```javascript
    <ContactCard 
        contact={{
            name: "Mr. Whiskerson", 
            imgUrl: "http://placekitten.com/300/200", 
            phone: "(212) 555-1234", 
            email: "mr.whiskaz@catnap.meow"
        }}
    />
```

We need to go from JS to JSX and to do that we using the double bracket notation - 
the first gets us into JS, the second gets is into the object. 
We use the same convention for writing out inline styles.

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

##State callback

State is asyncronous so it may run at the same time other functions get run. In order to ensure the state as been set
before calling some function, we can use a callback on setState:

```javascript
    this.setState({
        queryType: queryVal,
        queryID: randomCityID
        }, () => this.getWeatherData()
    )
```

## Working with forms

By using the name prop in the form itself, then matching the name in state, we can collect the values in state and use them:


```javascript
    function

    class App extends Component {
        constructor() {
            super()
            this.state = {
                firstName: "",
                lastName: "",
                job: ""
            }
            this.handleChange = this.handleChange.bind(this)
        }
        
        handleChange(event) {
            /*
                This line effectively adds a reference to the values as
                event.target. We can then use a simple name:value pairing 
                in setState as seen below. 

                Notice we need a ternary to identify checkboxes on their
                own. This is because are true/false and we don't need 
                their value
            */
            const {name, value, type, checked} = event.target
            type === "checkbox" ? 
                this.setState({
                    [name]: checked
                })
            :
            this.setState({
                [name]: value
            }) 
        }
        
        render() {
            return (
                <form>
                    <input 
                        type="text" 
                        value={this.state.firstName} 
                        name="firstName" 
                        placeholder="First Name" 
                        onChange={this.handleChange} 
                    />
                    <br />
                    <input 
                        type="text" 
                        value={this.state.lastName} 
                        name="lastName" 
                        placeholder="Last Name" 
                        onChange={this.handleChange} 
                    />
                    <input 
                        type="text" 
                        value={this.state.job} 
                        name="job" 
                        placeholder="Job" 
                        onChange={this.handleChange} 
                    />
                    <h1>{this.state.firstName} {this.state.lastName}</h1>
                    <h2>{this.state.job}</h2>
                </form>
            )
        }
    }

    export default App
```

### Handling form changes

#### Check boxes

Most form elements in expose a value property so the state can be set using the [name] of the element and the value that's been entered. Select boxes are a bit in that they just hold true or false. To hand this, our handleChange function needs a bit more login:

```javascript
    handleChange(event) {
        const {name, value, type, checked} = event.target
        type === "checkbox" ? this.setState({ [name]: checked }) : this.setState({ [name]: value })
    }
```
    

## setState, prevState and bind

Whenever we want a class method to be able to modify the state, we need 
to bind that method to the class. Below, handClick gets bound.


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

Above we're passing in a function we prevState as an argument than adding one to the count

## Two way data binding

Sometimes a component might need to change the state in the main class. To do this we can use
events and props. First we render the component and pass in the class function as a prop:

```javascript
    <LocationForm
        query={this.state.query} 
        handleChange={this.handleChange}
        getWeatherData={this.getWeatherData}
    />
```

We can then call the function in the functional component and interact with the state:

```javascript
  let handleChange = function(event) {
    props.handleChange(event)
  }

  or

  const handleChange = event => {
    props.handleChange(event)
  }

  return (
    <div className="location-form">
      <form>
        <input 
          type="text" 
          name="query" 
          value={props.query} 
          placeholder="Enter a location..."
          onChange={handleChange} 
        /> 
``



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
        const productsList = productsData.map( product => <Product key={product.id} name={product.name} />

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

## Meme Generator app - uses State, componentDidMount, forms

```javascript
    import React, {Component} from "react"

    class MemeGenerator extends Component {
        constructor() {
            super()
            this.state = {
                topText: "",
                bottomText: "",
                randomImg: "http://i.imgflip.com/1bij.jpg",
                allMemeImgs: []
            }
            this.handleChange = this.handleChange.bind(this)
            this.handleSubmit = this.handleSubmit.bind(this)
        }
        
        componentDidMount() {
            fetch("https://api.imgflip.com/get_memes")
                .then(response => response.json())
                .then(response => {
                    const {memes} = response.data
                    this.setState({ allMemeImgs: memes })
                })
        }
        
        handleChange(event) {
            const {name, value} = event.target
            this.setState({ [name]: value })
        }
        
        handleSubmit(event) {
            event.preventDefault()
            const randNum = Math.floor(Math.random() * this.state.allMemeImgs.length)
            const randMemeImg = this.state.allMemeImgs[randNum].url
            this.setState({ randomImg: randMemeImg })
        }
        
        render() {
            return (
                <div>
                    <form className="meme-form" onSubmit={this.handleSubmit}>
                        <input 
                            type="text"
                            name="topText"
                            placeholder="Top Text"
                            value={this.state.topText}
                            onChange={this.handleChange}
                        /> 
                        <input 
                            type="text"
                            name="bottomText"
                            placeholder="Bottom Text"
                            value={this.state.bottomText}
                            onChange={this.handleChange}
                        /> 
                    
                        <button>Gen</button>
                    </form>
                    <div className="meme">
                        <img src={this.state.randomImg} alt="" />
                        <h2 className="top">{this.state.topText}</h2>
                        <h2 className="bottom">{this.state.bottomText}</h2>
                    </div>
                </div>
            )
        }
    }

    export default MemeGenerator
```