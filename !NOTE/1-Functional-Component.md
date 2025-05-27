# 🔑 Functional Component

 
### ✅ What Is a Functional Component in React?
A functional component is a JavaScript function that returns JSX (React elements). It is:

- Simple and readable
- Used to define UI
- Can use hooks (like useState, useEffect)
- Accepts props as an argument

## Syntax of Functional Component
```jsx 
function Welcome() {
  return <h1>Hello, AN Mamun!</h1>;
}

// Or using arrow function:
 
const Welcome = () => {
  return <h1>Hello, AN Mamun!</h1>;
};
```

## 🧪 Example with props
```jsx 
function Greet(props) {
  return <h2>Welcome, {props.name}!</h2>;
}

// Or using destructuring: 
const Greet = ({ name }) => {
    return  <h2>Welcome, {name}!</h2>;  
};


// Usage
<Greet name="Mamun" />

```

## 🧲 Example with useState (Functional + State)
```jsx 
import { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <h2>Count: {count}</h2>
      <button onClick={() => setCount(count + 1)}>Increase</button>
    </div>
  );
}
```

## How to Use Functional Component in App
```jsx 
import React from 'react';
import ReactDOM from 'react-dom/client';
import App from './App.jsx';

ReactDOM.createRoot(document.getElementById('root')).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```
App.jsx

```jsx 
import Greet from './components/Greet';
import Counter from './components/Counter';

function App() {
  return (
    <>
      <Greet name="AN Mamun" />
      <Counter />
    </>
  );
}

export default App;
```

✅ Key Points to Remember 
- JSX	- HTML-like syntax used in React
- Functional 	- Component	A JS function returning JSX
- Props	- 	Data passed from parent to child component
- useState		- Hook to handle local component state