<h1>Code Breakdown</h1>

<p>This page should cover all the steps that were taken to create the JWT with PERN web application. Code snippets will be shown and explained, along with screenshots of how the database looks on PostgreSQL, analyzing how the database connects to the website in the localhost, and how JWT was used to implement authentication.</p>

<h2>Server</h2>

<h3>(Server) index.js:</h3>

<p>
express and app: Importing the Express framework and creating an instance of the application.
cors: Importing the CORS middleware to handle cross-origin requests.
pool: Importing the database connection from ./db.
Middleware:
express.json(): Middleware to parse incoming JSON requests.
cors(): Middleware to enable CORS, allowing the frontend to make requests to this backend from different origins.
Routes:
/auth: Mounting the JWT authentication routes from ./routes/jwtAuth.
/dashboard: Mounting the dashboard routes from ./routes/dashboard.
Server Start:
app.listen(5000, ...): Starting the Express server on port 5000 and logging a message to the console when the server starts.
</p>

<h3>db.js</h3>

<p>
Pool: Importing the Pool class from the pg module, which is used to create a pool of database connections.
pool: Creating a new instance of the Pool class with the following configurations:
user: The username to connect to the PostgreSQL database.
password: The password for the PostgreSQL user.
host: The hostname or IP address of the PostgreSQL server (in this case, it's localhost).
port: The port number on which the PostgreSQL server is running (default is 5432).
database: The name of the PostgreSQL database to connect to (in this case, it's "jwt").
module.exports: Exporting the pool instance so that it can be imported and used in other files, such as your main application file (app.js) or any route handlers that require database access.
</p>

<h3>App.js</h3>

<p>
useState: Declaring a state variable isAuthenticated to track whether the user is authenticated or not.
setAuth: A function to update the isAuthenticated state variable.
isAuth: An asynchronous function to check if the user is authenticated by sending a request to the server with the JWT token stored in localStorage.
useEffect: Using useEffect to call the isAuth function when the component mounts.
Router and Routes: Using BrowserRouter, Routes, and Route from react-router-dom to set up the application's routing.
Routes: Defining the application's routes:
/ and /login: Display the Login component if the user is not authenticated, otherwise navigate to /dashboard.
/register: Display the Register component if the user is not authenticated, otherwise navigate to /login.
/dashboard: Display the Dashboard component if the user is authenticated, otherwise navigate to /login.
Navigate: Using Navigate from react-router-dom to navigate to different routes based on the authentication status.
toast.configure(): Configuring toast notifications to be used throughout the application.
</p>

<h2>Client</h2>

<h3>(Client) index.js</h3>

<p>
React: Importing the main React library.
ReactDOM: Importing the ReactDOM library, which is used to render React components to the DOM.
'./index.css': Importing the CSS file for styling.
App: Importing the main App component of the application.
ReactDOM.createRoot(document.getElementById('root')): Creating a new React root with the root DOM element, which is an asynchronous API to render React components.
root.render: Rendering the App component inside the React root. The <React.StrictMode> wraps the App component to enable React's strict mode, which helps identify potential problems in the application's code.
</p>




### <h3>(Server) index.js</h3>

<details>
<summary>Click to expand code</summary>

```js

// Importing required modules
const express = require("express");
const app = express();
const cors = require("cors");
const pool = require("./db");  // Importing the database connection

// Middleware
app.use(express.json());  // Middleware to parse JSON requests
app.use(cors());  // Middleware to enable CORS (Cross-Origin Resource Sharing)

// Routes

// Authentication routes for registering and logging in users
app.use("/auth", require("./routes/jwtAuth"));

// Dashboard route to access user dashboard
app.use("/dashboard", require("./routes/dashboard"));

// Start the server
app.listen(5000, () => {
    console.log("Server is running on port 5000");  // Logging a message when the server starts
});

```
</details>

### <h3>db.js</h3>

<details>
<summary>Click to expand code</summary>

```js

const Pool = require("pg").Pool;  // Importing the Pool class from the 'pg' module

// Creating a new Pool instance with database connection configurations
const pool = new Pool({
    user: "postgres",       // Database user
    password: "1234",       // Database password
    host: "localhost",      // Database host
    port: 5432,             // Database port
    database: "jwt"         // Database name
});

// Exporting the pool instance to be used in other files
module.exports = pool;


```
</details>

<hr>

### <h3>App.js</h3>

<details>
<summary>Click to expand code</summary>

```js

import React, { Fragment, useState, useEffect } from 'react';
import './App.css';

import { toast } from 'react-toastify';  // Importing toast notifications
import 'react-toastify/dist/ReactToastify.css';

import { BrowserRouter as Router, Routes, Route, Navigate } from "react-router-dom";  // Importing routing components

// Components
import Dashboard from "./components/Dashboard";
import Login from "./components/Login";
import Register from "./components/Register";

toast.configure();  // Configuring toast notifications

function App() {

  const [isAuthenticated, setIsAuthenticated] = useState(false);  // State to track authentication status

  // Function to set authentication status
  const setAuth = (boolean) => {
    setIsAuthenticated(boolean);
  };

  // Function to check if user is authenticated
  async function isAuth() {
    try {
      const response = await fetch("http://localhost:5000/auth/is-verify", {
        method: "GET",
        headers: { token: localStorage.token }  // Sending the JWT token stored in localStorage
      });

      const parseRes = await response.json();

      // Setting isAuthenticated based on the response
      parseRes === true ? setIsAuthenticated(true) : setIsAuthenticated(false);
    } catch (err) {
      console.error(err.message);
    }
  }

  useEffect(() => {
    isAuth();  // Calling isAuth function when the component mounts
  });

  return (
    <Fragment>
      <Router>
        <div className="container">
          <Routes>
            {/* Route to display Login component if not authenticated, otherwise navigate to Dashboard */}
            <Route exact path="/" element={!isAuthenticated ? <Login setAuth={setAuth} /> : <Navigate to="/dashboard" />} />
            
            {/* Route to display Login component if not authenticated, otherwise navigate to Dashboard */}
            <Route exact path="/login" element={!isAuthenticated ? <Login setAuth={setAuth} /> : <Navigate to="/dashboard" />} />
            
            {/* Route to display Register component if not authenticated, otherwise navigate to Login */}
            <Route exact path="/register" element={!isAuthenticated ? <Register setAuth={setAuth} /> : <Navigate to="/login" />} />
            
            {/* Route to display Dashboard component if authenticated, otherwise navigate to Login */}
            <Route exact path="/dashboard" element={isAuthenticated ? <Dashboard setAuth={setAuth} /> : <Navigate to="/login" />} />
          </Routes>
        </div>
      </Router>
    </Fragment>
  );
}

export default App;


```
</details>

<hr>

### <h3>(Client) index.js</h3>

<details>
<summary>Click to expand code</summary>

```js

import React from 'react';
import ReactDOM from 'react-dom/client';
import './index.css';
import App from './App';

// Creating a new React root with the root DOM element
const root = ReactDOM.createRoot(document.getElementById('root'));

// Rendering the App component inside the React root
root.render(
  <React.StrictMode>  {/* Enabling React's strict mode */}
    <App />  {/* Rendering the App component */}
  </React.StrictMode>
);


```
</details>

<hr>

### <h3>EditTodo.js</h3>

<details>
<summary>Click to expand code</summary>

```js

import React, { Fragment, useState } from "react";

// EditTodo component
const EditTodo = ({ todo }) => {

    // State variable to store the description of the todo item
    const [description, setDescription] = useState(todo.description);

    // Function to update the description of the todo item
    const updateDescription = async (e) => {
        e.preventDefault(); // Preventing the default form submission behavior
        try {
            const body = { description }; // Creating a body object with the updated description
            // Sending a PUT request to update the todo item with the new description
            const response = await fetch(`http://localhost:5000/todos/${todo.todo_id}`, {
                method: "PUT",
                headers: { "Content-Type": "application/json" },
                body: JSON.stringify(body)
            });

            window.location = "/"; // Redirecting to the homepage after successful update
        } catch (err) {
            console.error(err.message); // Logging any errors to the console
        }
    }

    // Rendering the EditTodo component
    return (
        <Fragment>
            {/* Button to trigger the modal */}
            <button type="button" className="btn btn-warning" data-toggle="modal" data-target={`#id${todo.todo_id}`}>
                Edit
            </button>

            {/* Modal for editing the todo item */}
            <div className="modal" id={`id${todo.todo_id}`} onClick={() => setDescription(todo.description)}>
                <div className="modal-dialog">
                    <div className="modal-content">

                        {/* Modal header */}
                        <div className="modal-header">
                            <h4 className="modal-title">Edit Todo</h4>
                            <button type="button" className="close" data-dismiss="modal" onClick={() => setDescription(todo.description)}>&times;</button>
                        </div>

                        {/* Modal body */}
                        <div className="modal-body">
                            {/* Input field to edit the description */}
                            <input type='text' className="form-control" value={description} onChange={e => setDescription(e.target.value)} />
                        </div>

                        {/* Modal footer */}
                        <div className="modal-footer">
                            {/* Edit button */}
                            <button type="button" className="btn btn-warning" data-dismiss="modal" onClick={e => updateDescription(e)}>Edit</button>
                            {/* Close button */}
                            <button type="button" className="btn btn-danger" data-dismiss="modal" onClick={() => setDescription(todo.description)}>Close</button>
                        </div>

                    </div>
                </div>
            </div>
        </Fragment>
    );
};

export default EditTodo; // Exporting the EditTodo component

```
</details>

<hr>

### <h3>InputTodo.js</h3>

<details>
<summary>Click to expand code</summary>

```js

import React, { Fragment, useState } from 'react';

// InputTodo component
const InputTodo = () => {

    // State variable to store the description of the todo item
    const [description, setDescription] = useState("");

    // Function to handle form submission
    const onSubmitForm = async e => {
        e.preventDefault(); // Preventing the default form submission behavior
        try {
            const body = { description }; // Creating a body object with the description
            // Sending a POST request to add a new todo item
            const response = await fetch("http://localhost:5000/todos", {
                method: "POST",
                headers: { "Content-Type": "application/json" },
                body: JSON.stringify(body)
            });

            window.location = "/"; // Redirecting to the homepage after successful addition
        } catch (err) {
            console.error(err.message); // Logging any errors to the console
        }
    };

    // Rendering the InputTodo component
    return (
        <Fragment>
            {/* Heading */}
            <h1 className="text-center mt-5">Pern Todo List</h1>

            {/* Form for adding a new todo item */}
            <form className="d-flex mt-5" onSubmit={onSubmitForm}>
                {/* Input field to enter the description of the new todo item */}
                <input type="text" className="form-control" value={description} onChange={e => setDescription(e.target.value)} />

                {/* Submit button */}
                <button className="btn btn-success">Add</button>
            </form>
        </Fragment>
    );
};

export default InputTodo; // Exporting the InputTodo component

```
</details>

<hr>

### <h3>ListTodos.js</h3>

<details>
<summary>Click to expand code</summary>

```js

import React, { Fragment, useEffect, useState } from "react";

import EditTodo from "./EditTodo";

// ListTodos component
const ListTodos = () => {

    // State variable to store the list of todos
    const [todos, setTodos] = useState([]);

    // Function to delete a todo item
    const deleteTodo = async (id) => {
        try {
            // Sending a DELETE request to delete the todo item with the specified id
            const deleteTodo = await fetch(`http://localhost:5000/todos/${id}`, {
                method: "DELETE"
            });

            // Updating the todos state to remove the deleted todo item
            setTodos(todos.filter(todo => todo.todo_id !== id));
        } catch (err) {
            console.error(err.message); // Logging any errors to the console
        }
    }

    // Function to fetch all todo items from the backend
    const getTodos = async () => {
        try {
            // Sending a GET request to fetch all todo items
            const response = await fetch("http://localhost:5000/todos");
            const jsonData = await response.json(); // Parsing the JSON response

            // Updating the todos state with the fetched todo items
            setTodos(jsonData);
        } catch (err) {
            console.error(err.message); // Logging any errors to the console
        }
    };

    // useEffect hook to fetch todos when the component mounts
    useEffect(() => {
        getTodos(); // Calling the getTodos function
    }, []);

    // Logging the todos to the console
    console.log(todos);

    // Rendering the ListTodos component
    return ( 
        <Fragment>
            {/* Table to display the list of todos */}
            <table className="table mt-5 text-center">
                <thead>
                    <tr>
                        <th>Description</th>
                        <th>Edit</th>
                        <th>Delete</th>
                    </tr>
                </thead>
                <tbody>
                    {/* Mapping through the todos array and rendering each todo as a table row */}
                    {todos.map(todo => (
                        <tr key={todo.todo_id}>
                            <td>{todo.description}</td>
                            <td>
                                {/* EditTodo component to edit the todo item */}
                                <EditTodo todo={todo} />
                            </td>
                            <td>
                                {/* Delete button to delete the todo item */}
                                <button className="btn btn-danger" onClick={() => deleteTodo(todo.todo_id)}>Delete</button>
                            </td>
                        </tr>
                    ))}
                </tbody>
            </table>
        </Fragment>
    );
};

export default ListTodos; // Exporting the ListTodos component

```
</details>

<hr>


