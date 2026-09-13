# 🧱 Dev Stack — Build Your Ideal Development Stack

Dev Stack is a single-page React app that lets you explore frontend, backend, database,
language, styling, and DevOps technologies side by side, and assemble your own personal
"stack" by picking the ones you'd use on your next project.

## 🛠️ Technologies Used

- **React 19** + **TypeScript** — component-based UI with static type checking
- **Vite** — fast development server and production bundler
- **Tailwind CSS v4** + **daisyUI** — utility-first styling and prebuilt UI primitives
- **React-Toastify** — toast notifications for stack actions
- **JSON** — local data file that drives the technology catalog

## ✨ Features

1. **Build-your-own stack:** Explore 15 technologies as responsive cards (3 columns on
   desktop, 2 on tablet, 1 on mobile) and add any of them to a live "Your Stack" sidebar
   with a single click — duplicate attempts are blocked with a warning toast, and each
   added card is disabled and marked "✓ Added to Stack".
2. **Instant feedback with toasts:** Every stack action — adding, attempting a duplicate,
   removing, and clearing all — triggers a react-toastify notification, so you always know
   an action registered.
3. **Data-driven and responsive by design:** The entire technology catalog is fetched at
   runtime from a local JSON file (with a real loading state) rather than hardcoded into a
   component, and the full layout — navbar, hero, cards, and sidebar — scales cleanly from
   mobile to desktop, unified by one shared gradient theme (orange → pink → violet) across
   the brand name, hero heading, and primary buttons.

## 🚀 Getting Started

```bash
npm install
npm run dev
```

- Live Site Link: https://kaleidoscopic-biscuit-460b82.netlify.app/

---

## 🧠 React Q&A

**1. What is JSX, and why is it used in React?**
JSX is a syntax extension for writing HTML-like markup directly inside JavaScript/TypeScript
files. React uses it because it makes the intended UI far easier to read than calling
`createElement` by hand — the shape of a component is visible at a glance, with regular JS
expressions embedded via `{}`.

**2. What is the difference between props and state?**
Props are values a component receives *from* its parent — from the component's own point of
view they're read-only (e.g. `technology`, `onAdd` passed to `TechnologyCard`). State is data
a component owns and manages itself via `useState`, and it can change over time as the user
interacts with the app (e.g. the `stack` array in `App`). Props flow downward; state lives
locally and drives re-renders when updated.

**3. What does the `useState` hook do, and where did you use it in this project?**
`useState` gives a function component a piece of state that survives across renders and
causes a re-render whenever it changes. It's used in `App.tsx` to hold `technologies`, the
user's `stack`, `isLoading`, and `error`, and in `Navbar.tsx` to track whether the mobile
menu is open.

**4. What does the `useEffect` hook do, and why did you need it to load the JSON data?**
`useEffect` runs side effects — code that goes beyond rendering, such as network calls —
after a component renders. Because data fetching shouldn't happen during render itself,
`App.tsx` uses `useEffect` with an empty dependency array to fetch `technologies.json` once
on mount and store the result in state.

**5. Why does every item in a `.map()` list need a unique `key` prop?**
The `key` prop helps React tell list items apart between renders, so it knows which ones were
added, removed, or reordered instead of rebuilding the whole list from scratch. Without a
stable, unique key (each technology's `id` here), React can mismatch items, causing subtle
bugs or lost component state.

**6. What is conditional rendering? Show one place you used it (example: the empty stack
message).**
Conditional rendering means showing different UI depending on a condition, instead of always
rendering the same markup. In `YourStack.tsx`, when `stack.length === 0` the component
displays a "Your stack is empty." placeholder; otherwise it maps over the stack and renders
the list of added technologies.

**7. How do you pass data from a parent component to a child component, and how does a
child send something back to the parent?**
A parent passes data down to a child as props — for example, `App` passes `technologies`,
`stackIds`, and the `onAdd` callback down to `TechnologyGrid`. To send data back up, the
parent passes a function down as a prop, and the child calls it with whatever it needs to
share; `TechnologyCard` calls the `onAdd(technology)` prop when its button is clicked, which
runs `handleAdd` back in `App`.
