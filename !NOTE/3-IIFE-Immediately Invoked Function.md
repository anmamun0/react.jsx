# IIFE - Immediately Invoked Function Expression 

##  What is an IIFE?
IIFE (Immediately Invoked Function Expression) is a JavaScript function that runs as soon as it's defined.

##   Why use IIFE in React/JSX?
In React JSX, you sometimes need to run logic or conditionals that return JSX — and normal if or switch statements can't be used directly inside JSX. 
That's where IIFE helps.<br><br>

✅ Basic Syntax:
```
in react

{(
   // write code
)()};
```

```js 
(function() {
  console.log("I run immediately!");
})();
Or using arrow function:

(() => {
  console.log("I run too!");
})();
```


## ✅ JSX Use Case: Conditional Rendering with IIFE

```jsx 
const ScoreCard = ({ score }) => (
  <div>
    {(() => {
      if (score >= 90) return <p>Grade: A+</p>;
      if (score >= 80) return <p>Grade: A</p>;
      if (score >= 70) return <p>Grade: B</p>;
      return <p>Grade: F</p>;
    })()}
  </div>
);
```
Explanation:
We're using an IIFE to run if logic and return different JSX depending on score.

## ✅ Use Case: Switch-Case in JSX (using IIFE)
```jsx 
const StatusLabel = ({ status }) => (
  <div>
    {(() => {
      switch (status) {
        case 'pending':
          return <span className="text-yellow-500">Pending</span>;
        case 'approved':
          return <span className="text-green-500">Approved</span>;
        case 'rejected':
          return <span className="text-red-500">Rejected</span>;
        default:
          return <span className="text-gray-500">Unknown</span>;
      }
    })()}
  </div>
);
```

## ✅ Use Case: Inline Calculations

```jsx
const BookPrice = ({ price, taxRate }) => (
  <div>
    Final Price: {(() => {
      const total = price + price * taxRate;
      return `$${total.toFixed(2)}`;
    })()}
  </div>
);
```

## IIFE Outside JSX (logic-only)

```jsx 
const result = (() => {
  const a = 5, b = 10;
  return a + b;
})();

console.log(result); // 15
```

#### ⚠️ Warning
Don’t overuse IIFE. It’s useful when you need logic and return value inline (especially JSX), but for longer logic or reusable code, prefer creating a separate function.

