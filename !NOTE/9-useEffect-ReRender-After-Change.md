## What is useEffect?
useEffect is a Hook that runs after the component renders. It's used for:

- Fetching data
- Setting up subscriptions
- Manually updating the DOM
- Working with timers, localStorage, etc.


🔧 Basic Syntax
```jsx 
import { useEffect } from "react";

useEffect(() => {
  // Your side effect logic here
}, [dependencies]);
```

## Dependency Array Rules
- No dependencies → Runs on every render
- Empty [] → Runs only once (like componentDidMount)
- With dependencies → Runs when any listed dependency changes





### Example 1: Log on Every Render

```jsx
import React, { useEffect } from 'react';

const Example = () => {
  useEffect(() => {
    console.log("Component rendered or updated!");
  });

  return <h1>Hello</h1>;
};
```
### Example 2: Run Only Once (ComponentDidMount)

```jsx 
useEffect(() => {
  console.log("Runs only once on mount");
}, []); // empty dependency array
```

### Example 3: Cleanup on Unmount
```jsx 
useEffect(() => {
  const timer = setInterval(() => {
    console.log("Running every second");
  }, 1000);

  return () => {
    clearInterval(timer); // cleanup
    console.log("Timer cleared on unmount");
  };
}, []);
```

📦 Example 4: With Dependencies

```jsx
const [count, setCount] = useState(0);

useEffect(() => {
  console.log(`Count changed: ${count}`);
}, [count]); // runs only when `count` changes
```


### Real-Life Use Case (API Fetch)

```jsx 
import React, { useEffect, useState } from 'react';

const UserList = () => {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    fetch('https://jsonplaceholder.typicode.com/users')
      .then(res => res.json())
      .then(data => setUsers(data));
  }, []);

  return (
    <ul>
      {users.map(user => <li key={user.id}>{user.name}</li>)}
    </ul>
  );
};
``` 

<br>
<br>
<br>

---




Let's go over several advanced and complex use cases with explanations and working examples.

## 0. After Change the value will re-render useEffect
```
import React, { useRef, useEffect, useState } from "react"; 

const Test = () => {
  const [change, setChange] = useState(0);

  useEffect(() => {
    alert('New Refresh ');
  }, [change]);

  const handleChange = () => {
    setChange(change + 1);
    console.log(change);
  }

  return <>
    <button onClick={handleChange} className="bg-blue-600 px-4 py-2 text-white m-2">Click</button>
  </>;
};

export default Test;
```

## 1. Fetching with Cleanup (AbortController)
If a user navigates away before the fetch completes, you should cancel the request to avoid memory leaks or unwanted state updates.

```jsx
useEffect(() => {
  const controller = new AbortController();

  fetch("https://jsonplaceholder.typicode.com/posts", {
    signal: controller.signal,
  })
    .then(res => res.json())
    .then(data => console.log(data))
    .catch(err => {
      if (err.name === "AbortError") {
        console.log("Fetch aborted");
      } else {
        console.error(err);
      }
    });

  return () => {
    controller.abort();
  };
}, []);
```

## 2. Window Resize Listener

```jsx 
const [windowWidth, setWindowWidth] = useState(window.innerWidth);

useEffect(() => {
  const handleResize = () => {
    setWindowWidth(window.innerWidth);
  };

  window.addEventListener('resize', handleResize);

  return () => {
    window.removeEventListener('resize', handleResize);
  };
}, []);
```

## Use case: Responsive UI components that depend on screen width.

## 3. Syncing State to LocalStorage

```jsx 
const [theme, setTheme] = useState("light");

useEffect(() => {
  localStorage.setItem("theme", theme);
}, [theme]);
```
📌 Use case: Automatically store user preferences locally.

## 4. Polling Data (setInterval)
```jsx 
useEffect(() => {
  const interval = setInterval(() => {
    console.log("Fetching new data...");
    // fetch data
  }, 5000);

  return () => clearInterval(interval);
}, []);
```
📌 Use case: Auto-refresh dashboards or real-time updates.

## 5. Track Mouse Position

```jsx 
const [coords, setCoords] = useState({ x: 0, y: 0 });

useEffect(() => {
  const updateCoords = (e) => {
    setCoords({ x: e.clientX, y: e.clientY });
  };
  window.addEventListener("mousemove", updateCoords);

  return () => {
    window.removeEventListener("mousemove", updateCoords);
  };
}, []);
```
📌 Use case: Custom cursor effects, drawing tools, games, etc.

## 6. Reacting to Route Changes (with React Router)

```jsx
import { useLocation } from 'react-router-dom';

const location = useLocation();

useEffect(() => {
  console.log("Route changed to:", location.pathname);
}, [location]);
```

📌 Use case: Analytics tracking, dynamic page titles, fetching based on routes.

## 7. Conditionally Run Effects
```jsx 
useEffect(() => {
  if (someCondition) {
    // run effect
  }
}, [someCondition]);
```
📌 Use case: Run logic only when a specific condition becomes true.

## 8. Chained Effects with Cleanup

```jsx 
useEffect(() => {
  const id = setTimeout(() => {
    console.log("1 second passed");
  }, 1000);

  return () => {
    clearTimeout(id);
  };
}, [dependency]);
```
📌 Use case: Debouncing search input, delayed actions.

## 9. Scroll Position Tracker
```jsx 
const [scrollY, setScrollY] = useState(0);

useEffect(() => {
  const handleScroll = () => {
    setScrollY(window.scrollY);
  };

  window.addEventListener('scroll', handleScroll);

  return () => window.removeEventListener('scroll', handleScroll);
}, []);
```
📌 Use case: Sticky navbars, scroll progress bars.

## 10. Run Effects in Response to Multiple Dependencies
```jsx 
useEffect(() => {
  console.log("name or age changed");
}, [name, age]);
```

📌 Use case: Conditionally reload data based on multiple inputs.

