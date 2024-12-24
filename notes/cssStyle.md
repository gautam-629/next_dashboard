# Next.js Styling Guide

## Overview

Documentation for CSS styling approaches in Next.js applications.

## Global Styles

- Import `global.css` in root layout (`app/layout.tsx`)
- Location: `/app/ui/global.css`
- Use for app-wide styles and CSS reset rules

## Styling Methods

### Tailwind CSS

```tsx
// Direct utility classes in markup
<div className="text-blue-500 p-4 flex">
```

- Pre-configured with create-next-app
- Utility classes applied directly in components
- Prevents style collisions
- Optimized bundle size

### CSS Modules

```tsx
// style.module.css
.button { background: blue; }

// Component.tsx
import styles from './style.module.css'
<button className={styles.button}>
```

- Scoped CSS per component
- Automatic unique class names
- Prevents style conflicts

### Conditional Styling with clsx

```tsx
import clsx from 'clsx'

<div className={clsx(
  'base-class',
  {
    'active-class': isActive,
    'disabled-class': isDisabled
  }
)}>
```

## Alternative Options

- Sass (.scss)
- CSS-in-JS: styled-jsx, styled-components, emotion

## Usage

Choose method based on project needs:

- Tailwind: Rapid development, utility-first approach
- CSS Modules: Traditional CSS with scoping
- Mixed approach: Combine methods as needed
