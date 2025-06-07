## React Router DOM

That's the standard library for routing in React apps. It allows you to build single-page applications (SPA) with navigation, nested routes, dynamic URLs, and more, without full page reloads.


<h6> 
 
What You'll Learn
 -  Setup & Installation
 -  Basic Routes (Modern Way)
 -  Layouts + Nested Routes
 -  Dynamic Routes
 -  Route Params
 -  Loader (fetching data)
 -  Error Handling
 -  Protected Routes
 -  Route Form Actions
 - Navigation (Link, NavLink, useNavigate)
</h6>
 
Installation
```bash
npm install react-router-dom
```

## 2. Basic Setup (React Router v6+)
```jsx 
// App.jsx
import { BrowserRouter, Routes, Route } from "react-router-dom";
import Home from "./pages/Home";
import About from "./pages/About";

export default function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<Home />} />          {/* http://localhost:3000/ */}
        <Route path="/about" element={<About />} />    {/* http://localhost:3000/about */}
      </Routes>
    </BrowserRouter>
  );
}
```




##  Folder Structure

```css 
src/
├── main.jsx
├── App.jsx (optional)
├── layout/
│   └── MainLayout.jsx
├── pages/
│   ├── Home.jsx
│   ├── About.jsx
│   ├── Contact.jsx
├── routes/
│   └── router.jsx
```

 
## 3. main.jsx (Entry File)
```jsx 
import React from "react";
import ReactDOM from "react-dom/client";
import { RouterProvider } from "react-router-dom";
import router from "./routes/router"; // custom file

ReactDOM.createRoot(document.getElementById("root")).render(
  <React.StrictMode>
    <RouterProvider router={router} />
  </React.StrictMode>
);
```

## 4. router.jsx – Modern Route Setup

```jsx 
import { createBrowserRouter } from "react-router-dom";
import MainLayout from "../layout/MainLayout";
import Home from "../pages/Home";
import About from "../pages/About";
import Contact from "../pages/Contact";

const router = createBrowserRouter([
  {
    path: "/",
    element: <MainLayout />,
    children: [
      { index: true, element: <Home /> },
      { path: "about", element: <About /> },
      { path: "contact", element: <Contact /> },
    ],
  },
]);

export default router;
```

## 5. MainLayout.jsx – Shared Layout
```jsx 
import { NavLink, Outlet } from "react-router-dom";

export default function MainLayout() {
  return (
    <div>
      <header>
        <NavLink to="/">Home</NavLink> |
        <NavLink to="/about">About</NavLink> |
        <NavLink to="/contact">Contact</NavLink>
      </header>
      <hr />
      <main>
        <Outlet /> {/* Pages render here */}
      </main>
    </div>
  );
}
```

## 6. Home.jsx, About.jsx, etc.

```jsx 
export default function Home() {
  return <h1>🏡 Home Page</h1>;
}
```
#####  Repeat for About.jsx, Contact.jsx.

## 7. Dynamic Routing with Params
Router Setup:

```jsx 
{
  path: "user/:id",
  element: <UserDetails />
}
```
Page:

```jsx 
import { useParams } from "react-router-dom";

export default function UserDetails() {
  const { id } = useParams();
  return <h2>User ID: {id}</h2>;
}
```
URL like /user/99 → prints User ID: 99.

## 8. Loader – Fetch data before component render
Router Setup:

```jsx 
{
  path: "posts",
  element: <Posts />,
  loader: () => fetch("https://jsonplaceholder.typicode.com/posts")
}
```
Page:

```jsx 
import { useLoaderData } from "react-router-dom";

export default function Posts() {
  const posts = useLoaderData();
  return (
    <ul>
      {posts.map(post => (
        <li key={post.id}>{post.title}</li>
      ))}
    </ul>
  );
}
```

## 9. Error Handling in Routes

```jsx 
{
  path: "/",
  element: <MainLayout />,
  errorElement: <h1>❌ 404 Not Found</h1>,
  children: [...]
}
```

Now if route doesn’t exist → shows error page.

## 10. Protected Route (like login required)
```jsx 
const PrivateRoute = ({ children }) => {
  const isLoggedIn = false;
  return isLoggedIn ? children : <Navigate to="/login" />;
};

// In router:
{
  path: "dashboard",
  element: <PrivateRoute><Dashboard /></PrivateRoute>
}
```

## 11. Form Actions
```jsx 
{
  path: "contact",
  element: <Contact />,
  action: async ({ request }) => {
    const formData = await request.formData();
    console.log("Form submitted:", formData.get("name"));
    return null;
  }
}
```

Form in Contact.jsx:
```jsx 
import { Form } from "react-router-dom";

export default function Contact() {
  return (
    <Form method="post">
      <input name="name" placeholder="Your Name" />
      <button type="submit">Send</button>
    </Form>
  );
}
```

## 12. useNavigate Example
```jsx 
import { useNavigate } from "react-router-dom";

const Go = () => {
  const navigate = useNavigate();
  return <button onClick={() => navigate("/about")}>Go to About</button>;
};
```

  Summary Table
<h6>
 
| Feature                 | Description                    |
| ----------------------- | ------------------------------ |
| `createBrowserRouter()` | Modern routing engine          |
| `RouterProvider`        | App-wide route support         |
| `Outlet`                | Shows child components         |
| `useNavigate()`         | Programmatic route navigation  |
| `useParams()`           | Get dynamic params from URL    |
| `useLoaderData()`       | Pre-fetch data                 |
| `Form + action()`       | Native form submission handler |
| `errorElement`          | Error boundary UI              |
</h6>



 <br>
 <br>
 <br>
 <br>
 
 ---
 
## createBrowserRouter() route object.

Here’s a breakdown with syntax, description, and example:

<h6> 
 
Route Object Properties in createBrowserRouter()

| Property           | Type       | Description                                                    |
| ------------------ | ---------- | -------------------------------------------------------------- |
| `path`             | `string`   | URL path for this route                                        |
| `element`          | `JSX`      | React element to render                                        |
| `children`         | `array`    | Nested route definitions                                       |
| `loader`           | `function` | Data fetching before render                                    |
| `action`           | `function` | Form submission handler                                        |
| `errorElement`     | `JSX`      | UI to render if loader/action errors                           |
| `index`            | `boolean`  | Whether this is the default index route                        |
| `handle`           | `object`   | Custom data or metadata for the route                          |
| `lazy`             | `function` | Lazy load the route component (like `import()` asynchronously) |
| `shouldRevalidate` | `function` | Control when a loader should re-run                            |
| `caseSensitive`    | `boolean`  | Match path with case sensitivity                               |
| `id`               | `string`   | Unique route identifier (for `useRouteLoaderData`, etc.)       |
</h6>

Example Explained

```jsx 
const router = createBrowserRouter([
  {
    path: "/",
    element: <MainLayout />,
    errorElement: <ErrorPage />,     // Renders when loader/action throws
    loader: rootLoader,              // Fetch initial app data
    children: [
      {
        index: true,
        element: <Home />,
      },
      {
        path: "dashboard",
        element: <Dashboard />,
        loader: dashboardLoader,
        action: dashboardAction,
        errorElement: <DashboardError />
      },
      {
        path: "login",
        element: <Login />,
        action: loginAction
      }
    ]
  }
]);
```

### Quick Overview

<h6>
  
| Key                | Example                                      | Description                                    |
| ------------------ | -------------------------------------------- | ---------------------------------------------- |
| `path`             | `"dashboard"`                                | Route URL path                                 |
| `index`            | `true`                                       | Default route at that level                    |
| `element`          | `<Component />`                              | What to render                                 |
| `loader`           | `async () => fetch()`                        | Load data before rendering                     |
| `action`           | `async ({ request }) => handleForm(request)` | Handle form POSTs                              |
| `children`         | `[ { path: "child" } ]`                      | Nested routes                                  |
| `errorElement`     | `<ErrorPage />`                              | Error UI                                       |
| `handle`           | `{ title: 'Dashboard' }`                     | Metadata (used in layout, breadcrumbs, etc.)   |
| `lazy`             | `() => import('./Dashboard')`                | Lazy load the route component                  |
| `id`               | `"dashboard-route"`                          | Use in `useRouteLoaderData("dashboard-route")` |
| `shouldRevalidate` | `({ currentUrl, nextUrl }) => true/false`    | Control loader re-runs                         |

</h6>

✅ App.jsx
```jsx 
import { RouterProvider, createBrowserRouter } from "react-router-dom";
import RootLayout from "./layouts/RootLayout";
import ErrorPage from "./components/ErrorPage";
import Home from "./pages/Home";
import Login from "./pages/Login";
import Dashboard, { dashboardLoader } from "./pages/Dashboard";
import { loginAction } from "./actions/loginAction";
import { rootLoader } from "./loaders/rootLoader";
import React from "react";

// Lazy load a page
const About = React.lazy(() => import("./pages/About"));

const router = createBrowserRouter([
  {
    path: "/",
    id: "root",
    element: <RootLayout />,
    loader: rootLoader,
    handle: {
      title: "My App",
      showNav: true,
    },
    errorElement: <ErrorPage />,
    children: [
      {
        index: true,
        element: <Home />,
      },
      {
        path: "dashboard",
        id: "dashboard",
        loader: dashboardLoader,
        element: <Dashboard />,
        shouldRevalidate: ({ currentUrl, nextUrl }) => {
          // Revalidate only when path actually changes
          return currentUrl.pathname !== nextUrl.pathname;
        },
        errorElement: <h1>Dashboard Error ❌</h1>,
      },
      {
        path: "login",
        element: <Login />,
        action: loginAction,
      },
      {
        path: "about",
        lazy: async () => {
          const { default: About } = await import("./pages/About");
          return { Component: About };
        },
      },
    ],
  },
]);

function App() {
  return <RouterProvider router={router} />;
}

export default App;
```

📁 Directory Structure
```css 
src/
├── App.jsx
├── actions/
│   └── loginAction.js
├── loaders/
│   └── rootLoader.js
├── layouts/
│   └── RootLayout.jsx
├── components/
│   └── ErrorPage.jsx
├── pages/
│   ├── Home.jsx
│   ├── Login.jsx
│   ├── Dashboard.jsx
│   └── About.jsx

```
### Sample of loader (e.g., rootLoader.js)

```js 
export async function rootLoader() {
  const res = await fetch("/api/user");
  if (!res.ok) throw new Error("Failed to load user data");
  return res.json();
}
```

### Sample of action (e.g., loginAction.js)

```js 
export async function loginAction({ request }) {
  const formData = await request.formData();
  const email = formData.get("email");
  const password = formData.get("password");

  // Send to server
  const res = await fetch("/api/login", {
    method: "POST",
    body: JSON.stringify({ email, password }),
    headers: { "Content-Type": "application/json" }
  });

  if (!res.ok) throw new Error("Login failed");
  return redirect("/dashboard");
}
```
<h6>
 
Key Points Recap
- loader: fetches data before rendering
- action: handles form submissions (usually POST)
- element: what component to show
- errorElement: shown if loader/action fails
- lazy: dynamically load route on-demand
- handle: holds custom metadata for routes
- shouldRevalidate: control re-fetching logic
- id: used with useRouteLoaderData('id')
- index: default nested route

</h6>

