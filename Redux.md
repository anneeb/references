# Redux

## Basics

State
  Define: let state = {key: value}
Action
  Define: let action = {type: string, key: value}

Reducer
  function changeState(state = {}, action){
    switch (action.type) {
      case 'INCREASE':
        return {count: state.count + 1}
        break
      default:
        return state
    }
  }

Dispatch
  Define: function dispatch(action) {state = changeState(state, action)}
  Initialize: dispatch({type: '@@INIT'})

Store
  function createStore() {
    let state
    return {
      dispatch: function(action) {
        state = reducer(state, action)
        render()
      },
      getState: function() {
        return state
      }
    }
  }
