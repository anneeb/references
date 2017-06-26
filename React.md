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

## Basics

Elements
  Create: React.createElement('tag', {properties}, [components])
    Class property: className
    For label: htmlFor
  Render: ReactDOM.render(element, target)
Components
  Create: React.createClass({component specifications})
    Required: render() {return element}
  ES6: class Name extends React.Component {render() {return element}}
JSX
  Create: class Name extends React.Component {render() {return (react html)}}
  Import: <ClassName />
