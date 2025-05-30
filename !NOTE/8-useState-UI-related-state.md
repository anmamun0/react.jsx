## What is useState() ?
useState is a React Hook that lets you add state to functional components.

### UNDER STANDING STATE
- In React, state refers to an object that holds data of your component
- When data changed component refresh automatically to reflect the changes

> Holds all Data State memory = UI View<br>
> if change state memory , automaticaly re-render the UI View

### WHY WE ARE USING
<h6> 
Spread Operator In State Object

- Step: 01 in React, the state object is intended to be immutable
- Step: 02 React encourages developers to follow the principle Of immutability when working with state,
- Step: 03 Which means that you should not directly mutate the state object, Instead, you create a new Object with the desired
changes and update the state with the new object.
- Step: 04 By following immutability. React can efficiently compare previous and current state objects to determine if a re.render is
necessary
- Step: 05 When you mutate the state object directly, React may not detect the changes correctly, leading to unexpected behavior.
Using the spread operator technique we are creating new object that maintains the previous state's values while making
the necessary modifications.
- Step: 07 This ensures that the state object remains immutable
- Step: 08 So, to always treat the state object as immutable and create a new object when updating state values, it ensures React can detect the change and trigger a re-render, maintaining predictable and reliable UI updates
</h6>

##### Syntax:
```js 
const [state, setState] = useState(initialValue);
```

`state`:  the current state value <br>
`setState`:  function to update the state <br>
`initialValue`:  the default value of the state <br>

## Simple Example
```jsx 
import React, { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <>
      <p>Clicked: {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click Me</button>
    </>
  );
}
```

## Common Data Types

```jsx
// 1. String 
const [name, setName] = useState("Mamun");
// 2. Number 
const [age, setAge] = useState(22);
// 3. Boolean 
const [isVisible, setIsVisible] = useState(false);
// 4. Array 
const [items, setItems] = useState([]);
// 5. Object 
const [user, setUser] = useState({ name: "", email: "" });
```

##  Update Object/Array State Properly

```jsx 
const [user, setUser] = useState({ name: "", email: "" });

const updateName = (e) => {
  setUser(prev => ({ ...prev, name: e.target.value }));
};
```

```jsx 
const [user, setUser] = useState({
                          fullname: "",
                          email: ""
                        });

const updateName = (e) => {
  setUser(prev => (
            { ...prev,
              fullname: 'Gest'
            }
    ));
};
```


## Controlled Input Example
```jsx 
const [email, setEmail] = useState("");
<input type="email" value={email} onChange={(e) => setEmail(e.target.value)} />
```

## Things to Remember
Concept	Description <br> 
Re-renders	Updating state causes the component to re-render <br> 
Async	setState is asynchronous <br> 
Immutable	Never directly mutate state (state++ ❌, use setState ✅) <br> 


## useState vs useRef

| Feature               | `useState`                                       | `useRef`                                                      |
| --------------------- | ------------------------------------------------ | ------------------------------------------------------------- |
| Purpose            | To store **reactive state** (triggers re-render) | To store **mutable data** that does **not** trigger re-render |
| Triggers re-render | ✅ Yes                                            | ❌ No                                                          |
| Keeps value        | ✅ Between renders                                | ✅ Between renders                                             |
| Used for           | UI-related state (input values, toggles, etc.)   | DOM access, storing timers, previous values                   |
| Updates on change  | ✅ Yes (component re-renders)                     | ❌ No (component does not re-render)                           |


<br>
<br>
<br>

---



## Mini Project Example: Todo List
```jsx 
function TodoList() {
  const [task, setTask] = useState("");
  const [todos, setTodos] = useState([]);

  const addTask = () => {
    if (task.trim()) {
      setTodos([...todos, task]);
      setTask("");
    }
  };

  return (
    <>
      <input value={task} onChange={e => setTask(e.target.value)} />
      <button onClick={addTask}>Add</button>
      <ul>
        {todos.map((t, i) => <li key={i}>{t}</li>)}
      </ul>
    </>
  );
}
```

 
## 1. Multi-Field Form Handling with State
Handle multiple inputs in a single object.

```jsx 
import { useState } from "react";

export default function ProfileForm() {
  const [form, setForm] = useState({
    name: "",
    email: "",
    age: "",
    country: "Bangladesh"
  });

  const handleChange = (e) => {
    const { name, value } = e.target;
    setForm(prev => ({ ...prev, [name]: value }));
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    console.log("📦 Form Data:", form);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input name="name" value={form.name} onChange={handleChange} placeholder="Name" />
      <input name="email" value={form.email} onChange={handleChange} placeholder="Email" />
      <input name="age" value={form.age} onChange={handleChange} placeholder="Age" />
      <select name="country" value={form.country} onChange={handleChange}>
        <option value="Bangladesh">Bangladesh</option>
        <option value="India">India</option>
        <option value="USA">USA</option>
      </select>
      <button type="submit">Submit</button>
    </form>
  );
}
```

## 2. Dynamic List (Add/Remove Items)

```jsx 
const TodoApp = () => {
  const [task, setTask] = useState("");
  const [list, setList] = useState([]);

  const addTask = () => {
    if (task) {
      setList([...list, { id: Date.now(), text: task }]);
      setTask("");
    }
  };

  const removeTask = (id) => {
    setList(list.filter(item => item.id !== id));
  };

  return (
    <>
      <input value={task} onChange={(e) => setTask(e.target.value)} />
      <button onClick={addTask}>Add</button>
      <ul>
        {list.map(item => (
          <li key={item.id}>
            {item.text} <button onClick={() => removeTask(item.id)}>❌</button>
          </li>
        ))}
      </ul>
    </>
  );
};
```

## 3. Tab Switcher Using State
```jsx 
const TabExample = () => {
  const [activeTab, setActiveTab] = useState("profile");

  return (
    <div>
      <button onClick={() => setActiveTab("profile")}>Profile</button>
      <button onClick={() => setActiveTab("settings")}>Settings</button>

      {activeTab === "profile" && <p>🧑 Profile Tab Content</p>}
      {activeTab === "settings" && <p>⚙️ Settings Tab Content</p>}
    </div>
  );
};
```

## 4. Password Visibility Toggle

```jsx 
const PasswordInput = () => {
  const [visible, setVisible] = useState(false);

  return (
    <>
      <input type={visible ? "text" : "password"} placeholder="Enter password" />
      <button onClick={() => setVisible(!visible)}>
        {visible ? "Hide" : "Show"}
      </button>
    </>
  );
};
```

## 5. Multi-Step Form Navigation
```jsx 
const MultiStepForm = () => {
  const [step, setStep] = useState(1);
  const [data, setData] = useState({
    name: "", email: "", password: ""
  });

  const next = () => setStep(step + 1);
  const back = () => setStep(step - 1);

  return (
    <>
      {step === 1 && (
        <>
          <input  placeholder="Name"  value={data.name}
            onChange={(e) => setData(prev => ({ ...prev, name: e.target.value }))}
          />
          <button onClick={next}>Next</button>
        </>
      )}
      {step === 2 && (
        <>
          <input   placeholder="Email"  value={data.email}
            onChange={(e) => setData(prev => ({ ...prev, email: e.target.value }))}
          />
          <button onClick={back}>Back</button>
          <button onClick={next}>Next</button>
        </>
      )}
      {step === 3 && (
        <>
          <input placeholder="Password" type="password" value={data.password}
            onChange={(e) => setData(prev => ({ ...prev, password: e.target.value }))}
          />
          <button onClick={back}>Back</button>
          <button onClick={() => console.log(data)}>Submit</button>
        </>
      )}
    </>
  );
};
```