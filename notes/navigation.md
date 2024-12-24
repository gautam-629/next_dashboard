# Next.js Navigation Guide

## Link Component

The `Link` component in Next.js is used for client-side navigation within your application. It ensures seamless page transitions without full page reloads.

### Example

```tsx
import Link from "next/link";

<Link href="/dashboard" className="your-styles">
  Dashboard
</Link>;
```

### Features

- **Client-side Navigation**: Navigates without a full page refresh.
- **Automatic Code Splitting**: Loads only the code needed for the current page.
- **Background Prefetching**: In production, prefetches linked routes when they appear in the viewport.
- **SEO-friendly**: Works well with server-side rendering and static site generation.

---

## Active Links Pattern

Highlight active links dynamically to improve user experience. Use the `usePathname` hook to determine the current route.

### Example

```tsx
"use client";

import { usePathname } from "next/navigation";
import clsx from "clsx";

export default function NavLinks() {
  const pathname = usePathname();

  return (
    <Link
      href="/path"
      className={clsx("base-styles", {
        "active-styles": pathname === "/path",
      })}
    >
      Link Text
    </Link>
  );
}
```

### Features

- Uses the `usePathname` hook to get the current route.
- Applies conditional styling using `clsx`.
- Enhances UX by visually indicating the active link.

---

## Navigation Features

- **Automatic Code Splitting**: Pages are split into isolated route segments, loading only the required code for each page.
- **Isolated Pages**: Errors in one page do not affect others.
- **Automatic Prefetching**: Linked routes are prefetched in production, enabling near-instant transitions.
- **SEO Optimized**: Pre-rendered HTML improves search engine rankings.

### Example of Code Splitting

```tsx
import Link from "next/link";

export default function Navigation() {
  return (
    <nav>
      <Link href="/home">Home</Link>
      <Link href="/about">About</Link>
      <Link href="/contact">Contact</Link>
    </nav>
  );
}
```

In this example, the `/home`, `/about`, and `/contact` pages are split into separate chunks and only loaded when needed.

---

## Best Practices

### 1. Use `Link` Instead of `<a>`

Always use the `Link` component for internal navigation. It avoids full page reloads and enables Next.js optimizations like prefetching.

### 2. Convert Components to `'use client'`

When using hooks like `usePathname`, ensure the component is marked with `'use client'`.

### 3. Implement Active Link Patterns

Highlight the active link dynamically for better UX using conditional classes.

### 4. Leverage Automatic Code Splitting

Design routes logically to maximize the benefits of code splitting and reduce the initial page load time.

---

## Notes

- Avoid placing non-interactive elements like `<div>` inside `Link`.
- Test navigation performance in production to experience prefetching.
- Combine `Link` with accessible elements for improved usability.
