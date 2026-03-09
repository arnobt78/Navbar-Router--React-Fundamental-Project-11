# Navbar Header - React, Vite, JavaScript, Custom CSS Fundamental Project 11

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![React](https://img.shields.io/badge/React-18.2-blue)](https://react.dev/)
[![Vite](https://img.shields.io/badge/Vite-4.1-646CFF)](https://vitejs.dev/)
[![React Router](https://img.shields.io/badge/React_Router-7.x-CA4245)](https://reactrouter.com/)
[![JavaScript](https://img.shields.io/badge/JavaScript-ES6%2B-F7DF1E)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)

- **Live Demo:** [https://navbar-link.vercel.app/](https://navbar-link.vercel.app/)

This project is a learning-focused, responsive Navbar built with React and Vite. It demonstrates client-side routing, React hooks (`useState`, `useRef`), dynamic layout (mobile toggle, desktop inline links), and reusable data-driven components. Use it as a reference for building navigation in single-page applications or as teaching material for React fundamentals.

---

## Table of Contents

- [Project Summary](#project-summary)
- [Features](#features)
- [Technology Stack](#technology-stack)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [Environment Variables](#environment-variables)
- [How to Run & Use](#how-to-run--use)
- [Routes & Pages](#routes--pages)
- [Components Walkthrough](#components-walkthrough)
- [Data & Configuration](#data--configuration)
- [Styling & Layout](#styling--layout)
- [Reusing in Other Projects](#reusing-in-other-projects)
- [Deployment](#deployment)
- [Scripts Reference](#scripts-reference)
- [Keywords & Concepts](#keywords--concepts)
- [Conclusion](#conclusion)
- [License](#license)

---

## Project Summary

Navbar Header is a **single-page application (SPA)** that provides a responsive navigation bar with:

- **Navigation links** (Home, About, Projects, Contact, Profile) driven by React Router — no full page reload, no 404s.
- **Social icon links** that open in a new tab (`target="_blank"` with `rel="noopener noreferrer"`).
- **Mobile-first layout**: hamburger toggle reveals links; on wider screens, links and social icons appear inline.
- **Stable layout** on load/refresh: reserved logo dimensions and min-heights prevent shifting or bouncing.

There is **no backend or API** in this project; it is frontend-only and suitable for learning and reuse as a navbar template.

---

## Features

- Responsive Navbar with toggleable links on mobile and inline layout on desktop (breakpoint 800px).
- Client-side routing via React Router: `/`, `/about`, `/projects`, `/contact`, `/profile` each render a demo page.
- Data-driven nav and social links: edit `src/data.jsx` to change links and icons without touching component JSX.
- React hooks: `useState` for toggle state, `useRef` for measuring link container height and animating expand/collapse.
- CSS transitions for smooth open/close and hover states; reserved logo/nav dimensions to avoid layout shift.
- Social links open in a new tab with secure `rel="noopener noreferrer"`.
- Built with Vite for fast dev server and HMR; ESLint for code quality.
- SEO-friendly metadata in `index.html` (title, description, Open Graph, Twitter Card, canonical URL).

---

## Technology Stack

| Category   | Technology |
|-----------|------------|
| UI        | React 18 (functional components, hooks) |
| Build     | Vite 4 |
| Routing   | React Router DOM 7 |
| Language  | JavaScript (ES6+), JSX |
| Styling   | Custom CSS (variables, flexbox, media queries) |
| Icons     | react-icons (Font Awesome subset) |
| Tooling   | ESLint 9 (flat config), Babel (ESLint parser + preset-react) |

**No backend, no database, no external API.** The app is static after build; routing is handled entirely on the client.

---

## Project Structure

```plaintext
11-navbar/
├── public/
│   └── vite.svg                 # Favicon / app icon
├── src/
│   ├── pages/                   # Route-level components (demo content)
│   │   ├── Home.jsx
│   │   ├── About.jsx
│   │   ├── Projects.jsx
│   │   ├── Contact.jsx
│   │   └── Profile.jsx
│   ├── App.jsx                  # Router setup + Navbar + Routes
│   ├── Navbar.jsx               # Responsive navbar (links + social icons)
│   ├── data.jsx                 # Nav links & social links (data only)
│   ├── main.jsx                 # Entry: React root, App, global CSS
│   ├── index.css                # Global + nav + page styles
│   └── logo.svg                 # Navbar logo asset
├── index.html                   # HTML shell, meta, script entry
├── vite.config.js               # Vite configuration
├── vercel.json                  # SPA fallback for deployment
├── eslint.config.js             # ESLint flat config (React + hooks)
├── package.json
└── README.md
```

**Key files:**

- **`App.jsx`** — Wraps the app in `BrowserRouter`, renders `Navbar` and `Routes` (one `Route` per page).
- **`Navbar.jsx`** — Renders logo, toggle button, collapsible links (from `data.jsx`), and social icons. Uses `Link` from React Router for in-app navigation.
- **`data.jsx`** — Exports `links` (path + label) and `social` (URL + icon component). Single source of truth for nav and social items.
- **`main.jsx`** — Mounts `App` into `#root` and imports `index.css`.
- **`index.css`** — Global reset/variables, nav styles, and `.page` content area styles.

---

## Getting Started

### Prerequisites

- **Node.js** 18+ (recommended)
- **npm** or **yarn**

### Installation

```bash
git clone https://github.com/arnobt78/Navbar--React-Fundamental-Project-11.git
cd Navbar--React-Fundamental-Project-11
npm install
```

---

## Environment Variables

This project **does not require any environment variables** to run. It is a static frontend with no API keys or server config.

If you later add an API or feature that needs config (e.g. base URL, feature flags), you can:

1. Create a `.env` file in the project root (do not commit it).
2. Use names prefixed with `VITE_` so Vite exposes them to the client:

```env
# Example (optional — not used in current codebase)
VITE_APP_TITLE=Navbar Header
VITE_API_BASE_URL=https://api.example.com
```

3. In code, read them via `import.meta.env.VITE_APP_TITLE` and `import.meta.env.VITE_API_BASE_URL`.
4. Add a `.env.example` file with placeholder values and document each variable in the README so others know what to set.

**Important:** Never commit `.env` or real secrets. Ensure `.env` is listed in `.gitignore` (or use a template like `.env.example` only).

---

## How to Run & Use

### Development

```bash
npm run dev
```

Then open the URL shown in the terminal (e.g. [http://localhost:5173](http://localhost:5173)). You can:

- Click **Home**, **About**, **Projects**, **Contact**, **Profile** — the URL and content below the navbar update without a full reload.
- Resize the window: below 800px the hamburger appears; above 800px links and social icons show inline.
- Click social icons to open external links in a new tab.

### Production build & preview

```bash
npm run build
npm run preview
```

`dist/` will contain the built app. `preview` serves it locally so you can test the production build and routing (e.g. direct visit to `/about`).

### Linting

```bash
npm run lint
npm run lint:fix   # Auto-fix where possible
```

---

## Routes & Pages

Routing is defined in `App.jsx` and uses React Router’s `BrowserRouter`, `Routes`, and `Route`. All paths are client-side; the server must serve `index.html` for every path (see [Deployment](#deployment)).

| Path       | Component   | Purpose (demo)        |
|-----------|-------------|------------------------|
| `/`       | `Home`      | Welcome + short intro |
| `/about`  | `About`     | Explains SPA routing   |
| `/projects` | `Projects` | Course/demo context    |
| `/contact`  | `Contact`  | Placeholder contact    |
| `/profile`  | `Profile`  | Placeholder profile    |

**How it works:** The navbar uses `<Link to={url}>` from `react-router-dom` for each item in `links` (from `data.jsx`). Clicking a link updates the URL and React Router renders the matching `Route`’s `element` (e.g. `<About />`) without a full page load.

---

## Components Walkthrough

### App.jsx

Sets up the router and layout: navbar always visible, route content below.

```jsx
import { BrowserRouter, Routes, Route } from 'react-router-dom';
import Navbar from './Navbar';
import Home from './pages/Home';
// ... other pages

const App = () => {
  return (
    <BrowserRouter>
      <main>
        <Navbar />
        <Routes>
          <Route path="/" element={<Home />} />
          <Route path="/about" element={<About />} />
          {/* ... */}
        </Routes>
      </main>
    </BrowserRouter>
  );
};
```

---

### Navbar.jsx

- **State:** `showLinks` (boolean) toggles mobile menu visibility.
- **Refs:** `linksContainerRef`, `linksRef` — used to read the height of the links list and set `links-container` height for a smooth expand/collapse (intentional ref read during render for this pattern; see comment and eslint-disable).
- **Data:** Imports `links` and `social` from `data.jsx` and maps over them.
- **Navigation:** Uses `<Link to={url}>` for `links` (in-app) and `<a href={url} target="_blank" rel="noopener noreferrer">` for `social` (external).

Snippet:

```jsx
import { Link } from "react-router-dom";
// ...
<ul className="links" ref={linksRef}>
  {links.map((link) => (
    <li key={link.id}>
      <Link to={link.url}>{link.text}</Link>
    </li>
  ))}
</ul>
// ...
{social.map((socialIcon) => (
  <li key={socialIcon.id}>
    <a href={socialIcon.url} target="_blank" rel="noopener noreferrer">
      {socialIcon.icon}
    </a>
  </li>
))}
```

---

### Page components (e.g. Home.jsx, About.jsx)

Each page is a simple presentational component: a `<section className="page">` with a title and short text. They exist to demonstrate routing and can be replaced with real content or more complex layouts.

Example:

```jsx
const Home = () => (
  <section className="page">
    <h1 className="page-title">Home</h1>
    <p className="page-text">Welcome! ...</p>
  </section>
);
export default Home;
```

---

## Data & Configuration

### data.jsx

**`links`** — array of `{ id, url, text }` for navbar items. `url` must match route paths in `App.jsx` (e.g. `/`, `/about`).

**`social`** — array of `{ id, url, icon }`. `icon` is a React element from `react-icons` (e.g. `<FaFacebook />`). These are used as external links.

To add a nav item or social icon: push a new object into the corresponding array and ensure a matching `Route` exists in `App.jsx` for new paths.

---

## Styling & Layout

- **Global:** `index.css` includes a small reset, CSS custom properties (colors, spacing, shadows, transitions), and base typography.
- **Nav:** `.nav-header`, `.nav-center`, `.links-container`, `.links`, `.social-icons`, `.logo`, `.nav-toggle` — with media query at `800px` to switch from stacked + toggle to horizontal layout. Logo has fixed width/height to avoid layout shift.
- **Page content:** `.page`, `.page-title`, `.page-text` for the routed content area (max-width, padding, typography).

No CSS-in-JS or component libraries; everything is plain CSS for clarity and reuse.

---

## Reusing in Other Projects

1. **Copy the Navbar:** Use `Navbar.jsx` + `data.jsx` + the nav-related parts of `index.css`. Replace the logo import with your own asset.
2. **Routing:** If you use React Router, keep `<Link to={url}>` for `links` and keep `Route` definitions in sync with `data.jsx` URLs.
3. **Data-driven links:** Extend `links` and `social` in `data.jsx`; add new routes in `App.jsx` and new page components as needed.
4. **Styling:** Copy the `:root` variables and nav/page block from `index.css` into your project and adjust colors/spacing to match your design.
5. **Icons:** Keep using `react-icons` or swap `social[].icon` to your own icon component or image.

---

## Deployment

- **Vercel:** The repo includes `vercel.json` with a single rewrite so all paths serve `index.html`, enabling client-side routing (e.g. direct access to `/about` works).
- **Other hosts:** Configure the server so that for any path (e.g. `/about`, `/profile`) it returns the same `index.html` (SPA fallback). Then the built JS from Vite will run and React Router will handle the path.

Build output is in `dist/` after `npm run build`. Point the host’s document root to `dist` (or the equivalent for your platform).

---

## Scripts Reference

| Command          | Description |
|------------------|-------------|
| `npm run dev`    | Start Vite dev server (HMR) |
| `npm run build`  | Production build into `dist/` |
| `npm run preview` | Serve `dist/` locally |
| `npm run lint`   | Run ESLint on project |
| `npm run lint:fix` | Run ESLint and apply fixes |

---

## Keywords & Concepts

- React (functional components, hooks)
- Vite (dev server, build, HMR)
- React Router (BrowserRouter, Routes, Route, Link)
- useState, useRef
- Conditional rendering, list mapping
- Responsive design (media queries, mobile toggle)
- CSS custom properties, transitions, flexbox
- react-icons
- Single-page application (SPA)
- Client-side routing
- Layout shift prevention (reserved dimensions)

---

## Conclusion

This project gives you a working, responsive navbar and simple SPA routing that you can run locally, build for production, and reuse or extend. It focuses on React fundamentals (state, refs, data-driven UI) and clear structure (data in `data.jsx`, routing in `App.jsx`, layout in `Navbar.jsx` and CSS). Use it as a template for other apps or as teaching material for React and Vite.

---

## License

This project is licensed under the [MIT License](https://opensource.org/licenses/MIT). Feel free to use, modify, and distribute the code as per the terms of the license.

## Happy Coding! 🎉

This is an **open-source project** - feel free to use, enhance, and extend this project further!

If you have any questions or want to share your work, reach out via GitHub or my portfolio at [https://www.arnobmahmud.com](https://www.arnobmahmud.com).

**Enjoy building and learning!** 🚀

Thank you! 😊

---
