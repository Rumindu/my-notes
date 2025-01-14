# Consolidating State Logic with a Reducer

1. **Explanation of existing `<Counter>`**
    ``` tsx 
    const Counter = () => {
      // state variable for storing count
      const [value, setValue] = useState(0);

      return (
        // 2 button for increase and reset the value 
        <div>
          Counter ({value})
          <button
            onClick={() => setValue(value + 1)}
          >
            Increment
          </button>
          <button
            onClick={() => setValue(0)}
          >
            Reset
          </button>
        </div>
      );
    };
    ```
    [source code](https://github.com/Rumindu/codeWithMosh-react-course-part2/blob/915fb8faa5b1750b9838f919cfb658bb3c3233e7/src/state-management/Counter.tsx)
    
    ![](assets/Pasted%20image%2020250114074452.png)

2. **Why we need a reducer** 
   - When program is getting grow, keeping track of how state get updated be little bit challenging. So then we use reducer
   - Using Reducer we can take all the state management logic outside of `<Counter>` component and centralized it inside the single function. 
   
3. **Create a Reducer Function**  
   - The reducer function takes 2 parameters: 
     1. `state`: the current state.
     2. `action`: an object describing what is the user trying to do.
   - Reducer takes current state and action and returns a new state
      ``` ts 
      // reducers/counterReducer.ts
      interface Action {
        // we can add string instead of union. but this approach is more type safe
        type: "INCREMENT" | "RESET";
      }

      export function counterReducer(state: number, action: Action): number {
        if (action.type === "INCREMENT")
          return state + 1;
        if (action.type === "RESET")
          return 0;
        return state;
      }
      ```
      [Source code](https://github.com/Rumindu/codeWithMosh-react-course-part2/blob/5c3b25b0584b95bfaabd37379e06556657c72c14/src/state-management/reducers/counterReducer.ts)

4. **Use the `useReducer` Hook in the Component**  
  
    ``` tsx 
    //Counter.tsx
    import { counterReducer } from "./reducers/counterReducer";

    const Counter = () => {
      //now we replace the useState with useReducer
      // const [value, setValue] = useState(0);
      const [value, dispatch] = useReducer(counterReducer, 0);
      return (
        //
        <div>
          Counter ({value})
          <button
            onClick={() => dispatch({ type: "INCREMENT" })}
          >
            Increment
          </button>
          <button onClick={() => dispatch({type:"RESET"})} >
            Reset
          </button>
        </div>
      );
    };
    ```
    [Source code](https://github.com/Rumindu/codeWithMosh-react-course-part2/blob/5c3b25b0584b95bfaabd37379e06556657c72c14/src/state-management/Counter.tsx)

   - Use the `dispatch` function to send actions to the reducer. Actions are objects containing a `type` property with a specific value (e.g., `"INCREMENT"` or `"RESET"`).

5. **TypeScript Enhancements**
    
   - Define a **union type** for the `type` property to ensure only valid actions are allowed.
   - TypeScript will catch errors when invalid actions are dispatched.
    ``` ts
    // counterReducer.ts
    export interface Action {
      type: "INCREMENT" | "RESET";
    }
    ```

6. **Benefits of Using Reducers**
   - Centralized state logic.
   - Better separation of concerns: Components focus on rendering; reducers handle state changes.
   - Reusability: Reducers can be shared across components with similar state management needs.
   - Type safety: TypeScript ensures that only valid actions and state updates are allowed.
---

# Creating Complex Actions with Reducers

1. **Introduction to the `<TaskList>` Component**
    
   - The component manages a list of tasks with functionality to add and delete tasks.
    ![](assets/Pasted%20image%2020250114114540.png)

    ``` tsx 
    //TaskList.tsx
    const TaskList = () => {
      const [tasks, setTasks] = useState<Task[]>([]);

      return (
        <>
          <button
            onClick={() =>
              setTasks([{ id: Date.now(), title: "Task " + Date.now() }, ...tasks])
            }
            className="btn btn-primary my-3"
          >
            Add Task
          </button>
          <ul className="list-group">
            {tasks.map((task) => (
              <li
                key={task.id}
                className="list-group-item d-flex justify-content-between align-items-center"
              >
                <span className="flex-grow-1">{task.title}</span>
                <button
                  className="btn btn-outline-danger"
                  onClick={() =>
                    // Creates new array only containing tasks where the condition was true
                    setTasks(tasks.filter((t) => t.id !== task.id))
                  }
                >
                  Delete
                </button>
                // ...

    ```
    [source code](https://github.com/Rumindu/codeWithMosh-react-course-part2/blob/3a185cf4c917f677e6e130f2c4f9e45c79d4d4d5/src/state-management/TaskList.tsx)
   - State updates (adding and deleting tasks) are handled directly in the component.
  
2. **Introducing a Reducer for Centralized State Management**
    
    - Reducers handle state updates based on dispatched actions.
    - Moves state logic outside the component into a single function.
  
3. **Defining the Reducer Function**
    ``` ts 
    // reducers/tasksReducer.ts
    interface Task {
      id: number;
      title: string;
    }

    interface AddTaskAction {
      type: "ADD";
      task: Task;
    }

    interface DeleteTaskAction {
      type: "DELETE";
      taskId: number;
    }

    type TaskAction = AddTaskAction | DeleteTaskAction;

    export function tasksReducer(tasks: Task[], action: TaskAction): Task[] {
      switch (action.type) {
        case "ADD":
          return [action.task, ...tasks];
        case "DELETE":
          return tasks.filter(task => task.id !== action.taskId);
        default:
          return tasks;
      }
    }

    ```
    [source code](https://github.com/Rumindu/codeWithMosh-react-course-part2/blob/19bd4cb254a589b13869909bf1f4cdec72349811/src/state-management/reducers/tasksReducer.ts)
      
    - **Key Concepts:**
      - Separate interfaces for each action type (`AddTaskAction` and `DeleteTaskAction`).
      - Use of `TaskAction` as a union of action types.
      - `switch` statement to handle actions.
  
4. **Refactoring the Component to Use the Reducer**
    ``` tsx 
    //TaskList.tsx
    const TaskList = () => {
      const [tasks, dispatch] = useReducer(tasksReducer, []);

      const addTask = () => {
        const newTask: Task = { id: Date.now(), title: `Task ${Date.now()}` };
        dispatch({ type: "ADD", task: newTask });
      };

      const deleteTask = (taskId: number) => {
        dispatch({ type: "DELETE", taskId: taskId });
      };

      return (
        <>
          <button onClick={addTask} className="btn btn-primary my-3">
            Add Task
          </button>
          <ul>
            {tasks.map((task) => (
              <li
                key={task.id}
              >
                {task.title}
                <button
                  onClick={() => deleteTask(task.id)}
                >
                  Delete
                </button>
                // ...

    ```
    [source code](https://github.com/Rumindu/codeWithMosh-react-course-part2/blob/19bd4cb254a589b13869909bf1f4cdec72349811/src/state-management/TaskList.tsx)


