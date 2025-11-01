# Create the Repo Locally and Connect the Repo to GitHub
- [ ] In VS Code Create a folder named `REACT-EXPRESS-TO-DO-APP`
- [ ] Create a folder named frontend
- [ ] Create a folder name backend
- [ ] Add a `.gitkeep` file to the frontend and the backend folder
    <details>
    <summary>Expand for instructions to accomplish the same using the terminal.</summary>
      
    - [ ] Open the terminal with `ctrl + j` and run the following commands **in this order**:
    - [ ] Run `pwd` to confirm you are in the `REACT-EXPRESS-TO-DO-APP` folder
    - [ ] Run `mkdir backend` to create a folder named backend
    - [ ] Run `cd backend` to change the working directory to the backend folder
    - [ ] Run `pwd` again and coonfirm it ends with `react-express-to-do-app/backend`
    - [ ] Run `touch .gitkeep` to ceate a .gitkeep file
    - [ ] Run `cd ..` to return the terminal to the root directory (in this case the `REACT-EXPRESS-TO-DO-APP` folder )
    - [ ] Run `pwd` to confirm you are in the `REACT-EXPRESS-TO-DO-APP` folder
    - [ ] Run `mkdir frontend` to create a folder named frontend
    - [ ] Run `cd frontend` to change the working directory to the frontend folder
    - [ ] Run `pwd` again and coonfirm it ends with `react-express-to-do-app/frontend`
    - [ ] Run `touch .gitkeep` to ceate a .gitkeep file
    </details>


- [ ] In your Github.com account, create a repo with the same name - `REACT-EXPRESS-TO-DO-APP`
- [ ] **Opt out** from adding a README, .gitignore, and license.
- [ ] Return to your local repo and open the terminal with `ctrl + j`
- [ ] Run `git init` on the local branch to initialize a .git 
- [ ] Run `git add .` to add all files to staging
- [ ] Run `git commit -m "adding initial folder structure for monorepo"` to commit the changes 
- [ ] Run `git branch -M main` to rename the current branch to main
- [ ] Run `git remote add origin https://github.com/<your github.com username>/REACT-EXPRESS-TO-DO-APP.git` to connect your local branch and your remote branch
- [ ] Run `git push -u origin main` to push your changes to the remote repo 


#### Checkpoint: You should now see the backend and frontend folders in your remote repo (aka in github.com).


# Set up the Backend
- [ ] Run `pwd` to confirm you are in the `REACT-EXPRESS-TO-DO-APP` folder; it should return a path that ends in `/react-express-to-do-app`
- [ ] Run `cd backend` to change directory on the terminal to the backend folder
- [ ] Run `npm init -y` to generate the package.json file 
- [ ] Run  `npm install express cors` to install express and cors
- [ ] Confirm you see a package-lock.json file
- [ ] Run `touch server.js` to add a server.js file inside the backend folder
- [ ] Copy this code into the server.js file
    - <details>
        <summary>Expand for the server.js code</summary>

        ### Server.js code

        ```js
            //THE URL to VIST is: http://localhost:3001/api/todos
            // Import required packages
            const express = require('express');
            const cors = require('cors');

            const app = express();
            const PORT = 3001;

            // Middleware to parse JSON request bodies
            app.use(express.json());

            // Enable CORS so React can make requests from port 5173
            app.use(cors());

            // In-memory todo storage
            let todos = [
            { id: 1, text: 'Learn React', completed: false },
            { id: 2, text: 'Learn Express', completed: false },
            { id: 3, text: 'Build a full stack app', completed: false }
            ];

            // Get all todos
            app.get('/api/todos', (req, res) => {
            res.json(todos);
            });

            // Get single todo by ID
            app.get('/api/todos/:id', (req, res) => {
            const todoId = parseInt(req.params.id);
            const todo = todos.find(t => t.id === todoId);

            if (todo) {
                res.json(todo);
            } else {
                res.status(404).json({ error: 'Todo not found' });
            }
            });

            // Add new todo
            app.post('/api/todos', (req, res) => {
            const newTodo = {
                id: Date.now(),
                text: req.body.text,
                completed: false
            };

            todos.push(newTodo);
            res.status(201).json(newTodo);
            });

            // Toggle todo completion
            app.put('/api/todos/:id', (req, res) => {
            const todoId = parseInt(req.params.id);
            const todo = todos.find(t => t.id === todoId);

            if (todo) {
                todo.completed = !todo.completed;
                res.json(todo);
            } else {
                res.status(404).json({ error: 'Todo not found' });
            }
            });

            // Delete todo
            app.delete('/api/todos/:id', (req, res) => {
            const todoId = parseInt(req.params.id);
            const initialLength = todos.length;

            todos = todos.filter(t => t.id !== todoId);

            if (todos.length < initialLength) {
                res.json({ message: 'Todo deleted successfully' });
            } else {
                res.status(404).json({ error: 'Todo not found' });
            }
            });

            app.listen(PORT, () => {
            console.log(`Server running on http://localhost:${PORT}`);
            });
        ```
</details>

Run `node server.js` to launch the backend code

#### Checkpoint: Go to [http://localhost:3001/api/todos](http://localhost:3001/api/todos) and confirm the app returns this: 
  <img width="505" height="471" alt="Screenshot 2025-11-01 173116" src="https://github.com/user-attachments/assets/f0776e17-e3f0-4aa8-8676-61497ee3d6bd" />



# Set up the Frontend


- [ ] Open a new terminal window with `ctrl + shift + backtick ` 
- [ ] Run `pwd` to confirm you are in the `REACT-EXPRESS-TO-DO-APP` folder
- [ ] Run `ls -a` and confirm you get back these:
    ```
    ./  ../  .git/  backend/  frontend/
    ```

- [ ] Run `npm create vite@latest frontend -- --template react` to create a a skeleton structure for a react project
- [ ] Chose **yes** for __Remove existing files and continue__
- [ ] Chose **no** for __Use rolldown-vite (Experimental)?:__
- [ ] Chose **yes** for __Install with npm and start now?__
- [ ] Delete the `src.js` folder and the `vite.config.js` file
- [ ] Add the `src.js ` folder provided in class
- [ ] Add the `vite.config.js` file provided in class

#### Checkpoint: Go to [http://localhost:5173/](http://localhost:5173/) and confirm you see a todo app that looks like this:
  <img width="1021" height="770" alt="Screenshot 2025-11-01 170049" src="https://github.com/user-attachments/assets/abf68192-fd54-48fe-9215-7ae728528a85" />




