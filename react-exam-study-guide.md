# React Internal Exam — Study Guide (2 Days Left)

---

## PART 1: What Matters Most (Priority Order)

Examiners love asking about things that are easy to test in a short answer or code-snippet format. Rank your effort like this:

**🔴 Must know cold (high weightage, always asked):**
- JSX rules (expressions, one root element, className, conditional rendering)
- Props (passing, destructuring, default props, props vs state)
- State (`useState`, immutability, batching)
- Events (`onClick`, `onChange`, synthetic events, passing arguments)
- Forms (controlled vs uncontrolled components)
- Hooks: `useState`, `useEffect` (dependency array!), `useRef`, `useContext`
- Fetching data (`useEffect` + `fetch`/`axios`, loading/error states)

**🟡 Important, commonly asked:**
- Styling methods (inline style object, CSS modules, className)
- React Router basics (`BrowserRouter`, `Routes`, `Route`, `useNavigate`, `Link`)
- Error Boundaries (concept + when used)
- `useMemo`, `useCallback` (what problem they solve)
- Fetch vs Axios differences

**🟢 Good to mention if time permits:**
- Built-in components: `Fragment (<>)`, `StrictMode`, `Suspense`
- React DevTools — how to inspect Components/Profiler tab
- Custom hooks

---

## PART 2: The 2-Day Battle Plan

### 🗓️ Day 1 (Today) — Build the base (~5-6 hrs)
| Time block | Focus |
|---|---|
| 1 hr | JSX + Built-in components + React DevTools |
| 1.5 hr | Props + State (write 3-4 tiny components by hand) |
| 1 hr | Events + Forms (build one controlled form yourself) |
| 1 hr | Styling approaches (all 3-4 methods, one example each) |
| 1.5 hr | Hooks: useState, useEffect deeply (this is the most-asked topic) |

**Rule:** Don't just read — type every example into a sandbox (CodeSandbox / StackBlitz) or even on paper. Muscle memory > re-reading.

### 🗓️ Day 2 (Tomorrow) — Depth + Practice (~5-6 hrs)
| Time block | Focus |
|---|---|
| 1 hr | Remaining hooks: useRef, useContext, useMemo, useCallback |
| 1 hr | Routing (React Router) |
| 45 min | Errors / Error Boundaries |
| 1 hr | Fetching & catching data patterns |
| 45 min | Fetch vs Axios comparison table (memorize) |
| Rest | Redo every code example from memory, no peeking. Write mock short-answers for each topic in 3-4 lines. |

### 🗓️ Exam Day — Morning revision (1-2 hrs)
- Skim ONLY the 🔴 list above.
- Re-read this guide's examples once, out loud if possible — explaining it to yourself (or a wall) cements it fast.
- Don't learn anything brand-new this morning; just reinforce.

**General exam strategy:** For theory questions, always structure your answer as: *(1) what it is → (2) why/when it's used → (3) a tiny code snippet*. Examiners give marks for code even in a "theory" question.

---

## PART 3: The Full Syllabus, Taught With Examples

### 1. React Foundation & JSX

React is a JavaScript library for building UIs out of reusable **components**. JSX is a syntax extension that lets you write HTML-like code inside JavaScript — it gets compiled to `React.createElement()` calls under the hood.

**Key JSX rules:**
- Must return **one root element** (or use a Fragment `<>...</>`)
- Use `className` instead of `class`
- Embed JS expressions with `{ }`
- Every tag must close (`<img />`, `<br />`)

```jsx
function Greeting() {
  const name = "Priya";
  return (
    <div className="box">
      <h1>Hello, {name}!</h1>
      {name.length > 3 ? <p>Nice long name</p> : <p>Short name</p>}
    </div>
  );
}
```

### 2. Built-in Components

| Component | Purpose |
|---|---|
| `<>...</>` (Fragment) | Group elements without adding an extra DOM node |
| `<StrictMode>` | Highlights potential bugs during development (runs effects twice in dev) |
| `<Suspense>` | Shows fallback UI while a component/data is loading (used with lazy loading) |

```jsx
<React.StrictMode>
  <Suspense fallback={<p>Loading...</p>}>
    <MyLazyComponent />
  </Suspense>
</React.StrictMode>
```

### 3. React DevTools — Inspecting Components

React DevTools is a browser extension with two tabs:
- **Components tab**: shows the component tree, lets you click a component to see its live **props** and **state**, and edit them on the fly to test behavior.
- **Profiler tab**: records renders and shows which components re-rendered and why (helps find performance issues).

*Exam tip: know that DevTools lets you inspect props/state in real time — that's usually the actual question.*

### 4. Props

Props (properties) are **read-only** data passed from a parent component to a child. They make components reusable.

```jsx
function UserCard({ name, age }) {
  return <p>{name} is {age} years old</p>;
}

function App() {
  return <UserCard name="Arun" age={21} />;
}
```
- Props flow **one-way** (parent → child).
- Can have default values: `function UserCard({ name = "Guest" })`.

### 5. React State

State is data **owned and managed by a component itself**, and when it changes, the component re-renders. Managed with the `useState` hook.

```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);
  return (
    <button onClick={() => setCount(count + 1)}>
      Clicked {count} times
    </button>
  );
}
```
**Key point:** State updates are **asynchronous and batched**, and you should never mutate state directly — always use the setter function.

**Props vs State (classic exam question):**
| Props | State |
|---|---|
| Passed from parent | Managed inside the component |
| Read-only | Can be changed |
| Cause child re-render when changed by parent | Cause own component to re-render |

### 6. Events

React uses **SyntheticEvents** — a wrapper around native browser events that works consistently across browsers.

```jsx
function Button() {
  function handleClick(e) {
    console.log("Clicked!", e.target);
  }
  return <button onClick={handleClick}>Click Me</button>;
}
```
To pass arguments: `onClick={() => handleClick(id)}` (use an arrow function, not `handleClick(id)` directly — that would call it immediately).

### 7. Forms

**Controlled component** = form input's value is driven by React state (most commonly used, and most commonly asked).

```jsx
function LoginForm() {
  const [email, setEmail] = useState("");

  function handleSubmit(e) {
    e.preventDefault(); // stops page reload
    console.log("Submitted:", email);
  }

  return (
    <form onSubmit={handleSubmit}>
      <input
        type="email"
        value={email}
        onChange={(e) => setEmail(e.target.value)}
      />
      <button type="submit">Login</button>
    </form>
  );
}
```
**Uncontrolled component**: uses a `ref` to read the DOM value directly instead of state — less common, mention it exists.

### 8. Styling React

| Method | Example |
|---|---|
| Inline style | `<div style={{ color: "red", fontSize: 20 }}>` (camelCase, object) |
| CSS classes | `<div className="card">` + a normal `.css` file |
| CSS Modules | `import styles from "./Card.module.css"` → `className={styles.card}` (scoped, avoids naming clashes) |
| Styled-components / Tailwind | Utility-based or CSS-in-JS, mention as modern alternatives |

```jsx
const style = { backgroundColor: "lightblue", padding: "10px" };
function Box() {
  return <div style={style}>Styled box</div>;
}
```

### 9. Hooks

Hooks let function components use state and lifecycle features.

- **`useState`** — local state (covered above).
- **`useEffect`** — runs side effects (data fetching, subscriptions, DOM updates) after render.

```jsx
useEffect(() => {
  console.log("Runs after every render");
}, []); // empty array = runs once, on mount only
```
Dependency array rules (**very frequently asked**):
- No array → runs after **every** render
- `[]` → runs **once** on mount
- `[value]` → runs when `value` changes

- **`useRef`** — persists a mutable value across renders without causing re-render; also used to directly access a DOM element.
```jsx
const inputRef = useRef(null);
<input ref={inputRef} />
// inputRef.current.focus()
```
- **`useContext`** — share data across many components without prop drilling.
- **`useMemo`** — memoizes an expensive **computed value** so it isn't recalculated every render.
- **`useCallback`** — memoizes a **function** so it isn't recreated every render (useful when passing callbacks to child components).

### 10. Routing (React Router)

```jsx
import { BrowserRouter, Routes, Route, Link } from "react-router-dom";

function App() {
  return (
    <BrowserRouter>
      <Link to="/about">About</Link>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
      </Routes>
    </BrowserRouter>
  );
}
```
- `useNavigate()` — programmatically change routes (e.g., after login).
- `useParams()` — read dynamic URL segments like `/user/:id`.

### 11. Errors — Error Boundaries

A class component that catches JS errors in its child tree and shows fallback UI instead of crashing the whole app.

```jsx
class ErrorBoundary extends React.Component {
  state = { hasError: false };
  static getDerivedStateFromError() {
    return { hasError: true };
  }
  render() {
    if (this.state.hasError) return <h2>Something went wrong.</h2>;
    return this.props.children;
  }
}
```
*Note: Error Boundaries must be class components (no hook equivalent yet) — a common trick question.*

### 12. Fetching and Catching Data

The standard pattern: fetch inside `useEffect`, track loading/error/data states.

```jsx
function Users() {
  const [users, setUsers] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    fetch("https://api.example.com/users")
      .then((res) => {
        if (!res.ok) throw new Error("Failed to fetch");
        return res.json();
      })
      .then((data) => setUsers(data))
      .catch((err) => setError(err.message))
      .finally(() => setLoading(false));
  }, []);

  if (loading) return <p>Loading...</p>;
  if (error) return <p>Error: {error}</p>;
  return <ul>{users.map((u) => <li key={u.id}>{u.name}</li>)}</ul>;
}
```

### 13. Fetch vs Axios

| Fetch (built-in) | Axios (library) |
|---|---|
| No installation needed | `npm install axios` |
| Must manually check `res.ok` and call `.json()` | Automatically parses JSON, `response.data` |
| No built-in request timeout | Supports timeouts easily |
| Basic error handling | Better error handling (catches HTTP errors automatically) |

```js
// Fetch
fetch(url).then(res => res.json()).then(data => console.log(data));

// Axios
axios.get(url).then(response => console.log(response.data));
```

---

## Quick Self-Check Before the Exam
Cover the guide and try to answer these out loud:
1. Difference between props and state?
2. What happens if you omit the dependency array in `useEffect`?
3. Controlled vs uncontrolled form input?
4. Why use `useCallback`?
5. How does an Error Boundary work, and why must it be a class?
6. Two differences between fetch and axios?

If you can answer these fluently, you're in good shape. Good luck! 🎯
