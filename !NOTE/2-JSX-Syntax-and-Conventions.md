
# 🔑 JSX Syntax & Conventions (With Examples)

## What is JSX?
##### JSX (JavaScript XML) is a syntax extension for JavaScript. It allows you to write HTML-like code inside JavaScript, which React compiles to React.createElement behind the scenes.

## 1. Always Return a Single Parent Element
You can't return multiple sibling elements without wrapping them.
 
```jsx 

return (
  <div>
    <h1>Hello</h1>
    <p>Welcome!</p>
  </div>
);

// or use Fragment:

return (
  <>
    <h1>Hello</h1>
    <p>Welcome!</p>
  </>
);

```
## 2. JSX Uses className Instead of class

```jsx 
return <div className="card">Hello</div>;
```

## 3. Use camelCase for Event Handlers and Properties

```jsx
✅ Good:
<button onClick={handleClick}>Click Me</button>

❌ Bad: 
<button onclick="handleClick()">Click Me</button>
```

## 4. JavaScript inside JSX: use {}
You can insert JS expressions in JSX using curly braces.

```jsx 
const name = "Mamun";

return <h2>Hello, {name}!</h2>; 
return <p>{10 + 20}</p>; // Output: 30

```

## 5. Self-closing Tags Must End with /

```jsx
✅ Correct:
<img src="logo.png" alt="Logo" />
<br />
<input type="text" />

❌ Incorrect:
<img src="logo.png" alt="Logo">

```

## 6. Conditionals: Use Ternary or Logical AND

```jsx 
{isLoggedIn ? <h2>Welcome</h2> : <h2>Please log in</h2>}
 
{books.length > 0 && <BookList books={books} />}
```
## 7. Inline Styles: Use Object Syntax

```jsx 
const style = {
  color: 'blue',
  fontSize: '20px'
};

return <h2 style={style}>Styled Text</h2>;
```

## 8. Comments in JSX
Use {/* ... */} inside JSX:

```jsx 
return (
  <div>
    {/* This is a comment */}
    <p>Hello World</p>
  </div>
);
```

## 9. JSX Cannot Return Multiple Elements Without Wrapping

```jsx
❌ Bad:
return (
  <h1>Hi</h1>
  <p>Bye</p>
);

✅ Good:
return (
  <>
    <h1>Hi</h1>
    <p>Bye</p>
  </>
);
```

## 10. JSX Expressions Must Return Something Valid

```jsx
❌ This will break:
{if (true) { return <h1>Hi</h1> }}


✅ Instead use ternary or conditionals outside:
{true ? <h1>Hi</h1> : null}
```


#### 🧪 Sample Functional Component with All Conventions

```jsx
const Welcome = ({ name }) => {
  const isLoggedIn = true;

  return (
    <div className="welcome">
      {/* Greet the user */}
      <h2 style={{ color: 'green' }}>Hello, {name}!</h2>

      {isLoggedIn ? (
        <p>You are logged in</p>
      ) : (
        <p>Please log in to continue</p>
      )}

      <img src="/logo.png" alt="Logo" />
    </div>
  );
};
```

<br>
<br>
<br>
<br>

---

##### Let’s now explore advanced JSX use cases across different patterns you’ll likely face while building real-world apps like your Library Management System.

🔥 1. Dynamic Rendering with Map (Lists)
```jsx 
const books = [
  { id: 1, title: 'React Basics' },
  { id: 2, title: 'Advanced JavaScript' },
];

const BookList = () => {
  return (
    <ul>
      {books.map((book) => (
        <li key={book.id}>{book.title}</li>
      ))}
    </ul>
  );
};
```

```jsx 
const books = ['Dhaka','Sylhet','Chattrogram','Barisal'];

const BookList = () => {
  return (
    <ul>
      {books.map((item,i) => (
        <li key={i.toString()}> {item} </li>
      ))}
    </ul>
  );
};
```

###### ✅ Always add a key when using .map() in JSX.

### 🔥 2. Conditional Rendering (Ternary & &&)

```jsx 
const UserStatus = ({ isLoggedIn }) => {
  return (
    <>
      <h2>{isLoggedIn ? 'Welcome back!' : 'Please log in.'}</h2>
      {isLoggedIn && <p>You have 3 new messages.</p>}
    </>
  );
};
```
### 🔥 3. JSX with Functions Inside Return

```jsx 
const formatUser = (user) => `${user.firstName} ${user.lastName}`;

const Profile = ({ user }) => {
  return <h2>Welcome, {formatUser(user)}!</h2>;
};
```

### 🔥 4. Inline Styles with Dynamic Logic

```jsx 
const Book = ({ available }) => {
  const style = {
    color: available ? 'green' : 'red',
    fontWeight: 'bold',
  };

  return <p style={style}>{available ? 'Available' : 'Out of stock'}</p>;
};
```

### 5. Nested Components
```jsx
const Header = () => <h1>Library System</h1>;
const Footer = () => <footer>© 2025</footer>;

const Layout = () => (
  <>
    <Header />
    <main>Dashboard goes here</main>
    <Footer />
  </>
);
```

### 6. Fragments to Avoid Extra <div>

```jsx
const BookSummary = () => {
  return (
    <>
      <h2>Book Name</h2>
      <p>Author: Someone</p>
    </>
  );
};
```

###  7. Array of JSX Elements

```jsx 
const alerts = [<p key="1">Low stock</p>, <p key="2">Pending dues</p>];

const AlertPanel = () => <div>{alerts}</div>;
```

###  8. Render Components Conditionally by Value

```jsx 
const UserType = ({ role }) => {
  switch (role) {
    case 'admin':
      return <p>Welcome Admin!</p>;
    case 'librarian':
      return <p>Welcome Librarian!</p>;
    case 'student':
      return <p>Welcome Student!</p>;
    default:
      return <p>Welcome Guest!</p>;
  }
};
```

###  9. Spread Operator for Props

```jsx
const BookDetails = ({ title, author, price }) => (
  <p>{title} by {author}, Price: ${price}</p>
);

const book = {
  title: 'Learn React',
  author: 'Mamun',
  price: 30
};

const App = () => <BookDetails {...book} />;
```

###  10. Short-Circuit Fallback with ||

```jsx 
const Welcome = ({ username }) => (
  <h1>Hello, {username || 'Guest'}!</h1>
);
```
### 11. JSX with Multiline Strings

```jsx 
const Description = () => (
  <p>
    {`This book contains:
- React Basics
- JSX Conventions
- Component Structure`}
  </p>
);
```
 

### 12. Dynamic Components

```jsx 
const components = {
  book: BookComponent,
  profile: ProfileComponent,
  dashboard: DashboardComponent,
};

const DynamicRenderer = ({ type }) => {
  const Component = components[type];
  return Component ? <Component /> : <p>Component not found</p>;
};
```

### 13. Conditional ClassNames
```jsx 
const BookItem = ({ available }) => {
  return (
    <div className={`book-card ${available ? 'bg-green-100' : 'bg-red-100'}`}>
      {available ? 'Available' : 'Unavailable'}
    </div>
  );
};
```

You can use libraries like classnames or clsx for even cleaner conditional class logic.

### 14. Render Props Pattern

```jsx 
const DataFetcher = ({ children }) => {
  const data = ['React', 'JSX', 'Hooks'];
  return children(data);
};

const MyComponent = () => (
  <DataFetcher>
    {(items) => (
      <ul>
        {items.map((item, i) => <li key={i}>{item}</li>)}
      </ul>
    )}
  </DataFetcher>
);
```

### 15. JSX + Ternary + Logical AND Together

```jsx
const UserMessage = ({ user }) => (
  <>
    {user ? (
      <p>Welcome, {user.name}</p>
    ) : (
      <p>Please log in</p>
    )}
    {user?.role === 'admin' && <p>Access: Admin Panel</p>}
  </>
);
```

### 16. Inline Immediately-Invoked Functions (IIFEs)

```jsx
const Status = ({ score }) => (
  <>
    {(() => {
      if (score > 80) return <p>Excellent</p>;
      if (score > 50) return <p>Good</p>;
      return <p>Try Again</p>;
    })()}
  </>
);
```

### 17. Destructuring + Default Props Inline

```jsx
const Book = ({ title = 'Unknown', author = 'Anonymous' }) => (
  <div>{title} by {author}</div>
);
```

### 18. Multiline JSX with Custom Wrapper

```jsx
const Alert = ({ children }) => (
  <div className="bg-yellow-100 p-3 rounded shadow">{children}</div>
);

// Usage
<Alert>
  <h3>Warning!</h3>
  <p>Book return deadline is tomorrow.</p>
</Alert>
```

### 19. Using .filter().map() Chain

```jsx
const BookList = ({ books }) => (
  <ul>
    {books
      .filter((book) => book.available)
      .map((book) => (
        <li key={book.id}>{book.title}</li>
      ))}
  </ul>
);
```

### 20. Reusable JSX Blocks

```jsx
const statusBadge = (status) => {
  return <span className={`badge ${status}`}>{status}</span>;
};

const Book = ({ title, status }) => (
  <div>
    {title} {statusBadge(status)}
  </div>
);
```

### 21. Complex Layout Composition with Fragments

```jsx
const Layout = () => (
  <>
    <Header />
    <Sidebar />
    <MainContent />
    <Footer />
  </>
);
```

<br>
<br>
<br>

---

## Why map() is used in JSX?
JSX is just syntactic sugar for React.createElement, and it needs to return a list of elements.

#### 🔹 map() returns a new array — perfect for JSX rendering.
 
```jsx 
{books.map(book => <li key={book.id}>{book.title}</li>)}
// This works because map() creates and returns a new array of JSX elements that React can render.
```
 
- ❌ for loop — doesn't return a value
- ❌ forEach() — returns undefined, is only for side-effects, not value transformation — so it’s not useful in JSX rendering.
 