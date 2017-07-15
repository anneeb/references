# React

## Set Up

Terminal
  Global,
    npm install -g create-react-app webpack
  In the project directory,
    npm install && npm start
Index.js
  import React from 'react'
  import ReactDOM from 'react-dom'

## Elements

Create
  Define: React.createElement('tag', {properties}, [components])
  Class property: className
  For label: htmlFor
Render
  Define: ReactDOM.render(element, target)

## Components

General
  Import: <Name />
  Methods: method = () => {}
Create class (deprecated)
  Define: React.createClass({render: function() {element}})
Container (ES6)
  Define: class Name extends React.Component {render() {return element or html}}
  Usage:
   - primarily concerned with how things work
   - rarely have any HTML markup of their own, aside from a wrapping <div>
   - often stateful
   - responsible for providing data and behavior to their children
Presentational (dummy, functional)
  Define: const Name = () => html
  Usage:
   - primarily concerned with how things look
   - probably only contain a render method
   - do not know how to load or alter the data that they render
   - rarely have any internally changeable state properties
   - best written as stateless functional components

# Components Lifecycles

Mounting
  Will: componentWillMount
    Can use: nextProps - no, nextState - no, setState - yes
    Called: just before mounting (once)
    Usage: sets initial state based on props
  Did: componentDidMount
    Can use: nextProps - no, nextState - no, setState - no
    Called: just after mounting (once)
    Usage: sets side effects
Updating
  Will receive props: componentWillReceiveProps
  	Can use: nextProps - yes, nextState - no, setState - yes
    Called: when it's going to receive new props (multiple)
    Usage: applying state changes based on new props
  Should update: shouldComponentUpdate
    Can use: nextProps - yes, nextState - yes, setState - no
    Called: whenever a re-render has been triggered (multiple)
    Usage: deciding whether a re-render should occur
  Will update: componentWillUpdate
    Can use: nextProps - yes, nextState - yes, setState - no
    Called: when new state and props are being received (multiple)
    Usage: prepare for update, dispatch any actions based on state change
  Did update: componentDidUpdate
    Can use: prevProps - yes, prevState - yes, setState - yes
    Called: just after the re-render has finished (multiple)
    Usage: any DOM updates following a render
Dismounting
  Will unmount: componentWillUnmount
  Can use: nextProps - no, nextState - no, setState - no
  Called: just before component is removed from the DOM (once)
  Usage: destroying any side effects set up in componentDidMount

## Props

General
  Define: <Component propName="propValue" />
  Spread: <Component {...card} />
Access
  Define: {this.props.propName}
  Select: const Component = ({prop, prop}) => {return()}
Default
  Define: Component.defaultProps = {key: value}
Children
  Define: <Component>children</Component>
  Access: this.props.children
  Map: React.Children.map(this.props.children, callback)
  Clone: React.cloneElement(element, {props})
  Count: React.Children.count(this.props.children)

## PropTypes

Set up
  Install: npm install prop-types
  Import: import PropTypes from 'prop-types'
Usage
  Define: Component.propTypes = {propName: PropTypes.type}
  Types: .bool, .string, .array, .object
  Is required: .isRequired
  Array of: .arrayOf(PropTypes.type)
  Shape: .shape({propName: PropTypes.type, propName: PropTypes.type})
  Custom: function(props, propName, componentName) {if (condition) {return new Error('error')}}

## State

Initial
  In class: state = {}
  In constructor: this.state = {}
Update
  In handler: this.setState(object, callback)
    Object assign: {key: Object.assign({}, this.state.key, {newKey: newValue})}
    Spread: {key: {...this.state.key, newKey: newValue}}

## Events

In component,
  Handling: method = (event) => {}
  Asynchronous: const target = event.target or event.persist()
In render,
  Reference: onClick={this.method}

## Forms

Controlled
  In constructor: this.state = {value: 'defaultValue'}
  In render: <input value={this.state.value} />
  In handler: this.setState({value: event.target.value})
Uncontrolled
  In render: <input defaultValue="defaultValue" ref={(input) => this.input = input} />
  In handler: this.input.value

## Routing

History
  Define: window.history
  Back: .back()
  Forward: .forward()
  New state and url: .pushState(state, title, url)
Router and routes
  Set up: import { BrowserRouter as Router, Route } from 'react-router-dom'
  Define: <Router><Route path="path" component={Component} /></Router>
Link
  Set up: import { Link } from 'react-router-dom'
  Define: <Link to="path">Text</Link>
NavLink
  Set up: import { NavLink } from 'react-router-dom'
  Define: <NavLink exact to="path" activeStyle={{prop: 'value'}}>Text</NavLink>
Switch
  Define: <Switch> </Switch>
