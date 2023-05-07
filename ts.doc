
import React, { useReducer } from "react";

const initialState = {
  todos: []
};

const reducer = (state, action) => {
  switch (action.type) {
    case "add":
      return {
        ...state,
        todos: [
          ...state.todos,
          {
            text: action.text,
            isEditing: false
          }
        ]
      };
    case "edit":
      return {
        ...state,
        todos: state.todos.map((todo, index) => {
          if (index === action.index) {
            return {
              ...todo,
              text: action.text,
              isEditing: false
            };
          }
          return todo;
        })
      };
    case "startEditing":
      return {
        ...state,
        todos: state.todos.map((todo, index) => {
          if (index === action.index) {
            return {
              ...todo,
              isEditing: true
            };
          }
          return todo;
        })
      };
    case "delete":
      return {
        ...state,
        todos: state.todos.filter((_, index) => index !== action.index)
      };
    default:
      return state;
  }
};

const ToDoList = () => {
  const [state, dispatch] = useReducer(reducer, initialState);

  const handleSubmit = event => {
    event.preventDefault();
    const inputText = event.target.todo.value;
    dispatch({ type: "add", text: inputText });
    event.target.todo.value = "";
  };

  const handleEdit = (index, event) => {
    event.preventDefault();
    const inputText = event.target.todo.value;
    dispatch({ type: "edit", index, text: inputText });
  };

  const handleDelete = index => {
    dispatch({ type: "delete", index });
  };

  const handleStartEditing = index => {
    dispatch({ type: "startEditing", index });
  };

  return (
    <div>
      <form onSubmit={handleSubmit}>
        <input name="todo" />
        <button type="submit">Add</button>
      </form>
      <ul>
        {state.todos.map((todo, index) => (
          <li key={index}>
            {todo.isEditing ? (
              <form onSubmit={event => handleEdit(index, event)}>
                <input name="todo" defaultValue={todo.text} />
                <button type="submit">Save</button>
              </form>
            ) : (
              <>
                <span>{todo.text}</span>
                <button onClick={() => handleStartEditing(index)}>
                  Edit
                </button>
                <button onClick={() => handleDelete(index)}>Delete</button>
              </>
            )}
          </li>
        ))}
      </ul>
    </div>
  );
};

export default ToDoList;