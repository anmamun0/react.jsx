# Passing Props - Properties

## What Are Props?
Props are short for properties. They are used to pass data from a parent component to a child component in React.

## Basic Example

🔹 1. Parent Component
```jsx
import React from 'react';
import Profile from './Profile';

const App = () => {
  return (
    <div>
      <h1>Library System</h1>
      <Profile name="AN Mamun" role="Librarian" />
    </div>
  );
};

export default App;
```

🔹 2. Child Component (Profile.js)
```jsx
const Profile = ({ name, role }) => {
  return (
    <div>
      <h2>Name: {name}</h2>
      <h3>Role: {role}</h3>
    </div>
  );
};
export default Profile;


// You can also use props object instead of destructuring:
const Profile = (props) => {
  return (
    <div>
      <h2>Name: {props.name}</h2>
      <h3>Role: {props.role}</h3>
    </div>
  );
};
```

✅ Output:
```pgsql 
Library System
Name: AN Mamun
Role: Librarian
```

<br>
<br>
<br>

---


 
Let’s explore many complex and practical use cases of passing props from a parent to child component in React — with real-world examples from systems like your Library Management System.

## 1. Passing Basic Props (String, Number, Boolean)
BookCard.js
```jsx 
const BookCard = ({ title, author, available }) => {
  return (
    <div>
      <h3>{title}</h3>
      <p>by {author}</p>
      <p>Status: {available ? "Available" : "Not Available"}</p>
    </div>
  );
};
```
Parent:
```jsx 
<BookCard title="React in Depth" author="Mamun" available={true} />
```

## 2. Passing Objects as Props

UserProfile.js 
```jsx
const UserProfile = ({ user }) => {
  return (
    <div>
      <h3>{user.name}</h3>
      <p>Email: {user.email}</p>
      <p>Role: {user.role}</p>
    </div>
  );
};
```

Parent:
```jsx 
const user = {
  name: "Mamun",
  email: "anmamun0@gmail.com",
  role: "Admin"
};

<UserProfile user={user} />
```

## 3. Passing Arrays and Rendering

BookList.js
```jsx 
const BookList = ({ books }) => {
  return (
    <ul>
      {books.map((book, idx) => (
        <li key={idx}>{book}</li>
      ))}
    </ul>
  );
};
```

Parent:
```jsx 
<BookList books={["Python", "React", "Data Science"]} />
```


## 4. Passing Functions (for Callback/Event)

BookAction.js
```jsx
const BookAction = ({ onBorrow }) => {
  return <button onClick={() => onBorrow("Clean Code")}>Borrow</button>;
};
```
Parent:

```jsx 
const handleBorrow = (title) => {
  alert(`Borrowed: ${title}`);
};

<BookAction onBorrow={handleBorrow} />
```

## 5. Conditional Props for Logic Control

Notification.js
```jsx
const Notification = ({ message, type }) => {
  const style = {
    color: type === "error" ? "red" : "green"
  };

  return <p style={style}>{message}</p>;
};
```

Parent:
```jsx
<Notification message="Login successful" type="success" />
<Notification message="Login failed" type="error" />
```

## 6. Children Props (passing JSX)
Card.js

```jsx
const Card = ({ title, children }) => {
  return (
    <div className="card">
      <h2>{title}</h2>
      <div>{children}</div>
    </div>
  );
};
```

Parent:
```jsx 
<Card title="Book Info">
  <p>Title: Deep Learning</p>
  <p>Author: Ian Goodfellow</p>
</Card>
```

## 7. Destructuring + Default Props

BookInfo.js
```jsx 
const BookInfo = ({ title = "Unknown", author = "Anonymous" }) => {
  return (
    <div>
      <h3>{title}</h3>
      <p>{author}</p>
    </div>
  );
};
```
Parent:
```jsx
<BookInfo />
<BookInfo title="React Handbook" />
```

## 8. Pass Multiple Data Types Together

Dashboard.js
```jsx
const Dashboard = ({ user, stats, onLogout }) => {
  return (
    <div>
      <h2>Welcome, {user.name}</h2>
      <p>Total Books: {stats.books}</p>
      <p>Borrowed: {stats.borrowed}</p>
      <button onClick={onLogout}>Logout</button>
    </div>
  );
};
```

Parent:
```jsx 
<Dashboard
  user={{ name: "Mamun" }}
  stats={{ books: 100, borrowed: 20 }}
  onLogout={() => console.log("Logged out")}
/>
```

## 9. Use Component as a Prop

Layout.js
```jsx
const Layout = ({ Header, Footer }) => {
  return (
    <>
      <Header />
      <main>Content here...</main>
      <Footer />
    </>
  );
};
```

Parent:
```jsx
import Navbar from "./Navbar";
import Footer from "./Footer";

<Layout Header={Navbar} Footer={Footer} />
```

## 10. Props with useState (Dynamic update)

Counter.js
```jsx 
const Counter = ({ count }) => {
  return <h3>Current Count: {count}</h3>;
};
```

Parent:
```jsx 
const App = () => {
  const [count, setCount] = useState(0);

  return (
    <>
      <Counter count={count} />
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </>
  );
};
```

## 11. Render Props Pattern (Function as Child)
Let the child decide what to render using a function.

🔧 Example: Reusable Hover Tracker
```jsx 
const HoverTracker = ({ children }) => {
  const [hovered, setHovered] = React.useState(false);
  return (
    <div onMouseEnter={() => setHovered(true)} onMouseLeave={() => setHovered(false)}>
      {children(hovered)}
    </div>
  );
};
```

Parent:
```jsx 
<HoverTracker>
  {(hovered) => <h2>{hovered ? "Mouse In" : "Mouse Out"}</h2>}
</HoverTracker>
```



## 12. Higher-Order Components (HOC)
HOC takes a component and returns a new one with additional props/logic.

withLogger HOC
```jsx 
const withLogger = (Component) => {
  return (props) => {
    console.log("Props: ", props);
    return <Component {...props} />;
  };
};
```

Parent: 
```jsx 
const Book = ({ title }) => <h2>{title}</h2>;
const BookWithLogger = withLogger(Book);

<BookWithLogger title="React Advanced" />
```


Summary Use Case Example's
<h6> 

- `String`	Name, role, label
- `Number`	ID, age, count
- `Boolean`	isAdmin, isAvailable
- `Object`	user, book, stats
- `Array`	books, users, notifications
- `Function`	onClick, onSubmit, onDelete
- `JSX`	Using children inside components
- `Component`	Passing Header, Footer, NavBar as prop

</h6>

 