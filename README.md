# This is part of the "Struggling with JavaScript" aka doc-js book

* https://leanpub.com/doc-js
* If you want to contribute to the book or join me as a coauthor pool, please get in contact mgalli at mgalli dot com subject "doc-js book"

# What about updating a component that uses map to filter out its element by a prop (sent from parent) 

Example of an inner component, child of another, that filter its child elements checking their props against parent-informed prop.

## Before

```
import React from 'react'
import PropTypes from 'prop-types'
import Todo from './Todo'

const TodoList = ({ todos, toggleTodo }) => (
  <ul>
    {todos.map(todo =>
      <Todo
        key={todo.id}
        {...todo}
        onClick={() => toggleTodo(todo.id)}
      />
    )}
  </ul>
)

TodoList.propTypes = {
  todos: PropTypes.arrayOf(PropTypes.shape({
    id: PropTypes.number.isRequired,
    detail: PropTypes.string.isRequired,
    list_id: PropTypes.number.isRequired,
    completed: PropTypes.bool.isRequired,
    text: PropTypes.string.isRequired
  }).isRequired).isRequired,
  toggleTodo: PropTypes.func.isRequired
}

export default TodoList

```

## After

```

import React from 'react'
import PropTypes from 'prop-types'
import Todo from './Todo'

const TodoList = ({ todos, toggleTodo, list_id }) => (
  <ul>
    {todos.map( (todo) => {
        if(todo.list_id===list_id) {
          return (  <Todo
                       key={todo.id}
                       {...todo}
                       onClick={() => toggleTodo(todo.id)}
                     />
                  )
        } else {
          return null;
        }

       }
    )}
  </ul>
)

TodoList.propTypes = {
  todos: PropTypes.arrayOf(PropTypes.shape({
    id: PropTypes.number.isRequired,
    detail: PropTypes.string.isRequired,
    list_id: PropTypes.number.isRequired,
    completed: PropTypes.bool.isRequired,
    text: PropTypes.string.isRequired
  }).isRequired).isRequired,
  toggleTodo: PropTypes.func.isRequired
}

export default TodoList

```
