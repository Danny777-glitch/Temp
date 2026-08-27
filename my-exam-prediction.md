# My Prediction — Likely Full Stack (React) Question Paper

This is my own read of what's most likely to appear, based on the question bank pattern + what's typically tested in a first React module. Treat it as a smart bet, not a guarantee — but if you only have time for one more pass, this is where I'd spend it.

---

## 🔴 Almost certainly asked (core, easy to test, appears in every set)

### 1. `useState` — counter/toggle style question
**Why I think this:** It's the single easiest concept to turn into a 2-mark *or* 16-mark question, and your question bank already has 2 variants of it (Book Tracker, Toggle Message).

```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);
  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
      <button onClick={() => setCount(count - 1)}>Decrement</button>
    </div>
  );
}
```
**Explanation:** `useState(0)` gives you a value (`count`) and a setter (`setCount`). Calling the setter triggers a re-render with the new value. State updates never mutate the old value directly — you always replace it.

---

### 2. `useEffect` + fetch — "load data from an API" question
**Why I think this:** This is the most "practical" looking question, and shows up in Part A (Q16) and as the core of any 8/16-mark data question. Very likely to reappear in some form (users, products, students — same skeleton).

```jsx
import { useState, useEffect } from "react";

function ProductList() {
  const [products, setProducts] = useState([]);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    fetch("https://fakestoreapi.com/products")
      .then((res) => res.json())
      .then((data) => {
        setProducts(data);
        setLoading(false);
      });
  }, []);

  if (loading) return <p>Loading...</p>;

  return (
    <ul>
      {products.map((p) => <li key={p.id}>{p.title}</li>)}
    </ul>
  );
}
```
**Explanation:** `useEffect(..., [])` runs once on mount — perfect for "fetch data when the page loads." Notice the pattern: fetch → set state → render based on state (loading vs loaded).

---

### 3. Props — parent passing data to child(ren)
**Why I think this:** Guaranteed at least one question (it's foundational and cheap to test at any mark level — 2, 8, or 16).

```jsx
function ProductCard({ name, price }) {
  return (
    <div className="card">
      <h3>{name}</h3>
      <p>₹{price}</p>
    </div>
  );
}

function ProductPage() {
  return (
    <div>
      <ProductCard name="Notebook" price={40} />
      <ProductCard name="Pen" price={10} />
    </div>
  );
}
```
**Explanation:** Data flows **one-way**, parent → child. `ProductPage` owns the values; `ProductCard` just receives and displays them via destructured props.

---

### 4. Controlled Form (login/registration style)
**Why I think this:** Forms show up repeatedly in your bank (email input, login form) — this is a favorite for 8-mark questions because it combines state + events + forms in one shot.

```jsx
import { useState } from "react";

function RegisterForm() {
  const [form, setForm] = useState({ name: "", email: "" });

  const handleChange = (e) => {
    setForm({ ...form, [e.target.name]: e.target.value });
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    console.log("Submitted:", form);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input name="name" value={form.name} onChange={handleChange} placeholder="Name" />
      <input name="email" value={form.email} onChange={handleChange} placeholder="Email" />
      <button type="submit">Register</button>
    </form>
  );
}
```
**Explanation:** Using one state **object** for the whole form (instead of one `useState` per field) is a slightly more advanced but commonly expected pattern — `[e.target.name]` dynamically picks which field to update, and `...form` spreads the rest unchanged.

---

## 🟡 Very likely (appeared clearly in your question bank, good 8-mark candidates)

### 5. `map()` + `key` prop — rendering a list
```jsx
function StudentList({ students }) {
  return (
    <ul>
      {students.map((s) => (
        <li key={s.id}>{s.name} - {s.marks}</li>
      ))}
    </ul>
  );
}
```
**Explanation:** `key` must be unique and stable (like a DB id) — it lets React's Virtual DOM diffing correctly track which list item changed, without re-rendering the entire list on every update.

---

### 6. React Router — basic multi-page setup
```jsx
import { BrowserRouter, Routes, Route, Link } from "react-router-dom";

function App() {
  return (
    <BrowserRouter>
      <Link to="/">Home</Link> | <Link to="/profile">Profile</Link>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/profile" element={<Profile />} />
      </Routes>
    </BrowserRouter>
  );
}
```
**Explanation:** `Routes`/`Route` swap out the visible component based on URL path, without a full page reload — this is what makes React apps "Single Page Applications" (SPA).

---

### 7. Error handling while fetching (try/catch or `.catch()`)
```jsx
useEffect(() => {
  fetch("https://api.example.com/data")
    .then((res) => {
      if (!res.ok) throw new Error("Something went wrong");
      return res.json();
    })
    .then((data) => setData(data))
    .catch((err) => setError(err.message));
}, []);
```
**Explanation:** `fetch` doesn't reject on HTTP errors (404/500) automatically — you must check `res.ok` and throw manually, which is a favorite "gotcha" examiners like to test.

---

### 8. Fetch vs Axios (comparison-style theory question)
| | Fetch | Axios |
|---|---|---|
| Setup | Built-in | `npm install axios` |
| JSON parsing | Manual `.json()` | Automatic `.data` |
| HTTP errors | Must check manually | Auto-rejects on error |

```jsx
axios.get("/api/users")
  .then((res) => setUsers(res.data))
  .catch((err) => console.log(err));
```

---

## 🟢 Possible (less certain, but appeared in your bank — worth a quick skim)

### 9. Inline vs External CSS
```jsx
<div style={{ color: "blue", padding: "10px" }}>Inline</div>
<div className="box">External (uses a .css file)</div>
```

### 10. Error Boundaries (class component)
```jsx
class ErrorBoundary extends React.Component {
  state = { hasError: false };
  static getDerivedStateFromError() {
    return { hasError: true };
  }
  render() {
    return this.state.hasError
      ? <h2>Something broke.</h2>
      : this.props.children;
  }
}
```

### 11. `useRef` for accessing DOM directly
```jsx
function FocusInput() {
  const inputRef = useRef(null);
  return (
    <div>
      <input ref={inputRef} />
      <button onClick={() => inputRef.current.focus()}>Focus</button>
    </div>
  );
}
```

---

## My honest guess of paper structure

| Section | My prediction |
|---|---|
| 2-mark questions | Mix of small `useState`/props/JSX snippets + 1 router + 1 fetch question |
| 8-mark question | Either the **form** (Q9-style) or **props/data flow** (Q3-style) — both are "safe" to test conceptually |
| 16-mark question | Almost certainly the **Book Tracker (state)** or **Employee List (map + keys)** — these test the most concepts in one component |

**If you only revise 4 things tonight, make it:** `useState`, `useEffect` + fetch, controlled forms, and `map()`/keys. Together they cover roughly 70% of what I'd expect on the paper.

Good luck tomorrow — you've got this.
