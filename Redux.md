# Redux

## Basics

Variables
  Store: const store = createStore(reducer)
  State: let state = {key: value}
Functions
  Create store:
    function createStore(reducer) {
      let state
      let listeners = []
      const getState = () => state
      const dispatch = (action) => {
        state = reducer(state, action)
        listeners.forEach(listener => listener())
      }
      const subscribe = (listener) => {
        listeners.push(listener)
      }
      dispatch({type: '@@INIT'})
      return {
        getState,
        dispatch,
        subscribe
      }
    }
  Reducer:
    function reducer(state = {}, action) {
      switch (action.type) {
        case 'TYPE':
          return {new state}
        default:
          return state
      }
    }
  Action:
    function action(data) {
      return {
        type: 'TYPE',
        payload: data
      }
    }


## React-Redux

Create store
  Set up: import { createStore } from 'redux'
  Dev tools:
    const store = createStore(reducer,
      window.(DELETE THE BACKSLASH)\__REDUX_DEVTOOLS_EXTENSION__ &&
      window.(DELETE THE BACKSLASH)\__REDUX_DEVTOOLS_EXTENSION__()
    )
Provider
  Set up: import { Provider } from 'react-redux'
  Usage: alerts Redux app when there has been a change in state and re-renders React app
  Define:
    ReactDOM.render(
      <Provider store={store}>
        <App />
      </Provider>,
      document.getElementById('root')
    )
Connect
  Set up: import { connect } from 'react-redux'
  Define: export default connect(mapStateToProps, mapDispatchToProps)(Component)
Map state to props
  Define: const mapStateToProps = (state) => {return {prop: state.key}}
Map dispatch to props
  Set up: import { bindActionCreators } from 'redux'
  Define:
    const mapDispatchToProps = (dispatch) => {
      return bindActionCreators({
        addItem: addItem
      }, dispatch)
    }
