✅ What is JSX?
JSX (JavaScript XML) is a syntax extension for JavaScript. It allows you to write HTML-like code inside JavaScript, which React compiles to React.createElement behind the scenes.

🔑 JSX Syntax & Conventions (With Examples)
1. Always Return a Single Parent Element
You can't return multiple sibling elements without wrapping them.

✅ Correct:

jsx
Copy
Edit
return (
  <div>
    <h1>Hello</h1>
    <p>Welcome!</p>
  </div>
);
or use Fragment:

jsx
Copy
Edit
return (
  <>
    <h1>Hello</h1>
    <p>Welcome!</p>
  </>
);
2. JSX Uses className Instead of class
jsx
Copy
Edit
return <div className="card">Hello</div>;
3. Use camelCase for Event Handlers and Properties
✅ Good:

jsx
Copy
Edit
<button onClick={handleClick}>Click Me</button>
❌ Bad:

jsx
Copy
Edit
<button onclick="handleClick()">Click Me</button>
4. JavaScript inside JSX: use {}
You can insert JS expressions in JSX using curly braces.

jsx
Copy
Edit
const name = "Mamun";

return <h2>Hello, {name}!</h2>;
jsx
Copy
Edit
return <p>{10 + 20}</p>; // Output: 30
5. Self-closing Tags Must End with /
✅ Correct:

jsx
Copy
Edit
<img src="logo.png" alt="Logo" />
<br />
<input type="text" />
❌ Incorrect:

jsx
Copy
Edit
<img src="logo.png" alt="Logo">
6. Conditionals: Use Ternary or Logical AND
jsx
Copy
Edit
{isLoggedIn ? <h2>Welcome</h2> : <h2>Please log in</h2>}
jsx
Copy
Edit
{books.length > 0 && <BookList books={books} />}
7. Inline Styles: Use Object Syntax
jsx
Copy
Edit
const style = {
  color: 'blue',
  fontSize: '20px'
};

return <h2 style={style}>Styled Text</h2>;
8. Comments in JSX
Use {/* ... */} inside JSX:

jsx
Copy
Edit
return (
  <div>
    {/* This is a comment */}
    <p>Hello World</p>
  </div>
);
9. JSX Cannot Return Multiple Elements Without Wrapping
Bad:

jsx
Copy
Edit
return (
  <h1>Hi</h1>
  <p>Bye</p>
);
Good:

jsx
Copy
Edit
return (
  <>
    <h1>Hi</h1>
    <p>Bye</p>
  </>
);
10. JSX Expressions Must Return Something Valid
❌ This will break:

jsx
Copy
Edit
{if (true) { return <h1>Hi</h1> }}
✅ Instead use ternary or conditionals outside:

jsx
Copy
Edit
{true ? <h1>Hi</h1> : null}
🧪 Sample Functional Component with All Conventions
jsx
Copy
Edit
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
Would you like a JSX practice task or want to build a page with JSX together?