# Navbar Header - React, Vite, JavaScript, Custom CSS Fundamental Project 11

- **Live Demo:** []()

---

## Table of Contents

- [Project Summary](#project-summary)
- [Features](#features)
- [Project Structure](#project-structure)
- [Technology Stack](#technology-stack)
- [Getting Started](#getting-started)
- [Usage & Learning Guide](#usage--learning-guide)
- [Component & Data Walkthrough](#component--data-walkthrough)
- [Code Examples](#code-examples)
- [Keywords & Concepts](#keywords--concepts)
- [Conclusion](#conclusion)

---

## Project Summary

This project is a step-by-step learning tool for React beginners. You will build a responsive Navbar that includes navigation links and social icons. The Navbar adapts its display for mobile and desktop views, teaching you about dynamic rendering, CSS transitions, and React hooks like `useState` and `useRef`. You will also learn how to use external assets and icons and handle component styling in a scalable manner.

---

## Features

- Responsive Navbar with toggleable links (mobile/desktop)
- Dynamic rendering of links and social icons from data arrays
- Uses React hooks (`useState`, `useRef`) for state and DOM access
- CSS transitions and dynamic heights for smooth UX
- Integration with `react-icons` for scalable vector graphics
- Built with Vite for fast development and HMR
- Fully commented code for educational purposes

---

## Project Structure

```plaintext
├── public/
│   └── logo.svg
├── src/
│   ├── App.jsx
│   ├── Navbar.jsx
│   ├── data.jsx
│   ├── index.css
│   └── main.jsx
└── README.md
```

**Key Files:**

- `App.jsx`: Main app component, renders Navbar.
- `Navbar.jsx`: Core component implementing all Navbar logic.
- `data.jsx`: Exports arrays for navigation links and social icons.
- `index.css`: Styles for the entire app.
- `logo.svg`: Project logo image.
- `main.jsx`: Entry point; renders `<App />` into the DOM.

_Note: Your structure may include other Vite/React boilerplate files._

---

## Technology Stack

- **React** (Functional Components, Hooks)
- **Vite** (for fast dev and build)
- **CSS** (custom properties, transitions, responsive design)
- **react-icons** (for iconography)
- **JavaScript (ES6+)**

---

## Getting Started

### Prerequisites

- Node.js (v18+ recommended)
- npm or yarn

### Installation

```bash
git clone https://github.com/arnobt78/Navbar--React-Fundamental-Project-11.git
cd Navbar--React-Fundamental-Project-11
npm install
```

### Running the App

```bash
npm run dev
```

Visit [http://localhost:5173](http://localhost:5173) (or as directed in terminal).

### Building for Production

```bash
npm run build
npm run preview
```

---

## Usage & Learning Guide

This project is structured to help you learn React step by step. You’ll start from a basic Navbar, then progressively add features and refactor for best practices.

1. **Start with the Data**: Open `data.jsx` to see how navigation links and social icons are structured as arrays of objects.
2. **Initial State Management**: In `Navbar.jsx`, use `useState` to show/hide links.
3. **Conditional Rendering**: Render links only when `showLinks` is true.
4. **Styling and CSS Classes**: Use CSS to hide/show elements and animate transitions.
5. **Dynamic Height with useRef**: Use `useRef` and `getBoundingClientRect` to animate the Navbar height smoothly.
6. **Responsive Design**: Use CSS media queries to adjust layout for desktop vs mobile.
7. **Icons and Images**: Import SVG logo and icons from `react-icons` into the Navbar.
8. **Final Touches**: Polish with social icons and finish responsive tweaks.

---

## Component & Data Walkthrough

### 1. `data.jsx`

Defines the navigation and social links:

```js
export const links = [
  { id: 1, url: "/", text: "home" },
  { id: 2, url: "/about", text: "about" },
  // Add more as needed
];

export const social = [
  { id: 1, url: "https://twitter.com/", icon: <FaTwitter /> },
  // Add more as needed
];
```

---

### 2. `Navbar.jsx`

**Initial Approach:**

```js
import { useState } from "react";
import { links, social } from "./data";
import logo from "./logo.svg";
import { FaBars } from "react-icons/fa";

const Navbar = () => {
  const [showLinks, setShowLinks] = useState(false);
  return (
    <nav>
      <div className="nav-header">
        <img src={logo} className="logo" alt="logo" />
        <button className="nav-toggle" onClick={() => setShowLinks(!showLinks)}>
          <FaBars />
        </button>
      </div>
      {showLinks && (
        <ul className="links">
          {links.map((link) => (
            <li key={link.id}>
              <a href={link.url}>{link.text}</a>
            </li>
          ))}
        </ul>
      )}
    </nav>
  );
};

export default Navbar;
```

---

**Dynamic Height Approach:**

```js
import { useState, useRef } from "react";
const Navbar = () => {
  const [showLinks, setShowLinks] = useState(false);
  const linksContainerRef = useRef(null);
  const linksRef = useRef(null);

  const linkStyles = {
    height: showLinks
      ? `${linksRef.current.getBoundingClientRect().height}px`
      : "0px",
  };

  return (
    <nav>
      <div className="nav-header">
        <img src={logo} className="logo" alt="logo" />
        <button className="nav-toggle" onClick={() => setShowLinks(!showLinks)}>
          <FaBars />
        </button>
      </div>
      <div
        className="links-container"
        ref={linksContainerRef}
        style={linkStyles}
      >
        <ul className="links" ref={linksRef}>
          {links.map((link) => (
            <li key={link.id}>
              <a href={link.url}>{link.text}</a>
            </li>
          ))}
        </ul>
      </div>
      <ul className="social-icons">
        {social.map((icon) => (
          <li key={icon.id}>
            <a href={icon.url}>{icon.icon}</a>
          </li>
        ))}
      </ul>
    </nav>
  );
};
```

---

## Code Examples

### Navbar CSS Snippet

```css
nav {
  background: var(--white);
  box-shadow: var(--shadow-1);
}

.nav-toggle {
  font-size: 1.5rem;
  color: var(--primary-500);
  background: transparent;
  border: none;
  cursor: pointer;
  transition: var(--transition);
}
.links-container {
  height: 0;
  overflow: hidden;
  transition: var(--transition);
}
.show-container {
  height: 10rem;
}
@media screen and (min-width: 800px) {
  .nav-toggle {
    display: none;
  }
  .links-container {
    height: auto !important;
  }
  .links {
    display: flex;
    gap: 0.5rem;
  }
  .social-icons {
    display: flex;
    gap: 0.5rem;
  }
  .links {
    display: flex;
    gap: 0.5rem;
  }
  .social-icons {
    display: flex;
    gap: 0.5rem;
  }
}
```

---

## Keywords & Concepts

- React
- Vite
- Functional Components
- useState
- useRef
- Conditional Rendering
- Array Mapping
- Responsive Design
- CSS Transitions
- React Icons
- Dynamic Styles
- Component Structure

---

## Conclusion

This project is a practical and accessible way to master React basics by building something real and useful. By following the steps and reviewing the code, you’ll learn how to manage UI state, render lists dynamically, use refs for DOM manipulation, and apply responsive styles. Tweak, extend, and experiment to deepen your understanding!

For questions or suggestions, feel free to open an issue or contribute.

---

Happy Learning! 🚀

---
