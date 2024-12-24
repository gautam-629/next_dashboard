# Next.js Layouts and Pages Guide

## File-System Based Routing

- Folders create route segments that map to URL paths
- Nested folders create nested routes
- Special files:
  - `page.tsx`: Makes route accessible
  - `layout.tsx`: Shared UI between pages

## Page Structure

```tsx
// app/dashboard/page.tsx
export default function Page() {
  return <div>Dashboard Content</div>;
}
```

- Each page corresponds to a route segment
- Must export default component
- Required for route to be accessible

## Layout System

### Root Layout

```tsx
// app/layout.tsx
export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html>
      <body>{children}</body>
    </html>
  );
}
```

- Required
- Shared across all pages
- Modify `<html>` and `<body>` tags
- Add global metadata

### Nested Layouts

```tsx
// app/dashboard/layout.tsx
export default function DashboardLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <div>
      <nav>Dashboard Nav</nav>
      <main>{children}</main>
    </div>
  );
}
```

- Wrap specific route segments
- Share UI between related pages
- Children render inside layout

## Key Features

- Partial Rendering: Only page content updates on navigation
- Colocation: Keep related files together
- Component Reuse: Share UI across routes
- Nested Layouts: Multiple layout levels possible

## Folder Structure Example

```
app/
├── layout.tsx        # Root layout
├── page.tsx         # Home page
└── dashboard/
    ├── layout.tsx   # Dashboard layout
    ├── page.tsx     # Dashboard page
    ├── customers/
    │   └── page.tsx # Customers page
    └── invoices/
        └── page.tsx # Invoices page
```
