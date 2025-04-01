Here's a structured step-by-step guide to building a **To-Do App** while learning React from the basics. Each step introduces key concepts incrementally.

---

## **Step 1: Setup React Project**

### 📌 **Concepts Learned**

- Installing Node.js and npm
- Creating a React app using Vite or Create React App
- Understanding the project structure

### ✅ **Steps**

1. **Install Node.js** (Skip if already installed)

   - Download from [nodejs.org](https://nodejs.org/)
   - Verify installation:
     ```sh
     node -v
     npm -v
     ```

2. **Create a new React project using Vite (preferred)**
   ```sh
   npm create vite@latest todo-app --template react
   cd todo-app
   npm install
   npm run dev
   ```

---

## **Step 2: Understanding Components and JSX**

### 📌 **Concepts Learned**

- Functional components
- JSX syntax
- Rendering UI

### ✅ **Steps**

1. **Create a `components` folder inside `src/`**
2. **Create `TodoItem.jsx`**
   ```jsx
   function TodoItem() {
     return <li>Sample Task</li>;
   }
   export default TodoItem;
   ```
3. **Use it inside `App.jsx`**

   ```jsx
   import TodoItem from "./components/TodoItem";

   function App() {
     return (
       <div>
         <h1>Todo List</h1>
         <ul>
           <TodoItem />
         </ul>
       </div>
     );
   }
   export default App;
   ```

---

## **Step 3: Props and Reusable Components**

### 📌 **Concepts Learned**

- Passing data via props
- Making components dynamic

### ✅ **Steps**

1. Modify `TodoItem.jsx` to accept a `task` prop:
   ```jsx
   function TodoItem({ task }) {
     return <li>{task}</li>;
   }
   export default TodoItem;
   ```
2. Update `App.jsx` to pass different tasks:
   ```jsx
   function App() {
     const tasks = ["Learn React", "Build a Todo App", "Deploy Project"];
     return (
       <div>
         <h1>Todo List</h1>
         <ul>
           {tasks.map((task, index) => (
             <TodoItem key={index} task={task} />
           ))}
         </ul>
       </div>
     );
   }
   export default App;
   ```

---

## **Step 4: State Management with `useState`**

### 📌 **Concepts Learned**

- `useState` Hook
- Handling user input

### ✅ **Steps**

1. **Create an input field to add tasks**

   ```jsx
   import { useState } from "react";
   import TodoItem from "./components/TodoItem";

   function App() {
     const [tasks, setTasks] = useState([]);
     const [newTask, setNewTask] = useState("");

     const addTask = () => {
       if (newTask.trim()) {
         setTasks([...tasks, newTask]);
         setNewTask(""); // Clear input field
       }
     };

     return (
       <div>
         <h1>Todo List</h1>
         <input
           type="text"
           value={newTask}
           onChange={(e) => setNewTask(e.target.value)}
           placeholder="Enter task"
         />
         <button onClick={addTask}>Add</button>
         <ul>
           {tasks.map((task, index) => (
             <TodoItem key={index} task={task} />
           ))}
         </ul>
       </div>
     );
   }
   export default App;
   ```

---

## **Step 5: Handling Events (Delete Task)**

### 📌 **Concepts Learned**

- Event handling in React
- Updating state

### ✅ **Steps**

1. **Modify `TodoItem.jsx` to accept a delete function**
   ```jsx
   function TodoItem({ task, onDelete }) {
     return (
       <li>
         {task} <button onClick={onDelete}>Delete</button>
       </li>
     );
   }
   export default TodoItem;
   ```
2. **Update `App.jsx` to handle deletion**

   ```jsx
   const removeTask = (index) => {
     setTasks(tasks.filter((_, i) => i !== index));
   };

   <ul>
     {tasks.map((task, index) => (
       <TodoItem key={index} task={task} onDelete={() => removeTask(index)} />
     ))}
   </ul>;
   ```

---

## **Step 6: Styling with CSS**

### 📌 **Concepts Learned**

- Adding CSS styles
- Inline and external styles

### ✅ **Steps**

1. **Create `App.css`**
   ```css
   body {
     font-family: Arial, sans-serif;
     text-align: center;
   }
   ul {
     list-style: none;
     padding: 0;
   }
   li {
     background: #f4f4f4;
     margin: 5px;
     padding: 10px;
     border-radius: 5px;
   }
   button {
     margin-left: 10px;
     background: red;
     color: white;
     border: none;
     padding: 5px;
     cursor: pointer;
   }
   ```
2. **Import `App.css` in `App.jsx`**
   ```jsx
   import "./App.css";
   ```

---

## **Step 7: Local Storage (Persist Data)**

### 📌 **Concepts Learned**

- `useEffect` Hook
- Storing and retrieving data in `localStorage`

### ✅ **Steps**

1. **Update `useEffect` to store data**

   ```jsx
   import { useState, useEffect } from "react";

   function App() {
     const [tasks, setTasks] = useState(() => {
       const savedTasks = localStorage.getItem("tasks");
       return savedTasks ? JSON.parse(savedTasks) : [];
     });
     const [newTask, setNewTask] = useState("");

     useEffect(() => {
       localStorage.setItem("tasks", JSON.stringify(tasks));
     }, [tasks]);

     const addTask = () => {
       if (newTask.trim()) {
         setTasks([...tasks, newTask]);
         setNewTask("");
       }
     };

     const removeTask = (index) => {
       setTasks(tasks.filter((_, i) => i !== index));
     };

     return (
       <div>
         <h1>Todo List</h1>
         <input
           type="text"
           value={newTask}
           onChange={(e) => setNewTask(e.target.value)}
           placeholder="Enter task"
         />
         <button onClick={addTask}>Add</button>
         <ul>
           {tasks.map((task, index) => (
             <li key={index}>
               {task} <button onClick={() => removeTask(index)}>Delete</button>
             </li>
           ))}
         </ul>
       </div>
     );
   }
   export default App;
   ```

---

## **Next Steps**

- **Step 8:** Convert the project to use React Context API for state management.
- **Step 9:** Integrate with Firebase for backend data storage.
- **Step 10:** Deploy the app using GitHub Pages or Vercel.

Would you like to continue with these steps, or do you want more details on any concept? 🚀
