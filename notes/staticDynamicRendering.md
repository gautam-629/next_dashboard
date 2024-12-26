# Static and Dynamic Rendering

## Overview

In the previous chapter, we discussed data fetching for the Dashboard Overview page and identified two key limitations:

1. Data requests are creating an unintentional waterfall
2. The dashboard is static, so data updates aren't reflected in the application

## Topics Covered

- Static rendering and its performance benefits
- Dynamic rendering and appropriate use cases
- Approaches to make your dashboard dynamic
- Slow data fetch simulation

## Static Rendering

Static rendering performs data fetching and rendering on the server at build time (during deployment) or during data revalidation. Users receive cached results when visiting the application.

### Benefits

- **Faster Websites**: Prerendered content can be cached and globally distributed for quick, reliable access worldwide
- **Reduced Server Load**: Cached content eliminates the need for dynamic content generation per request
- **SEO**: Prerendered content is more accessible to search engine crawlers, potentially improving rankings

### Use Cases

Static rendering works well for:

- UI with no data
- Data shared across users (e.g., blog posts, product pages)

### Limitations

Not ideal for dashboards with personalized, frequently updated data.

## Dynamic Rendering

Dynamic rendering generates content on the server for each user at request time (during page visits).

### Benefits

- **Real-Time Data**: Displays current data with frequent updates
- **User-Specific Content**: Easily serves personalized content (dashboards, profiles)
- **Request Time Information**: Accesses request-time data (cookies, URL search parameters)

## Simulating Slow Data Fetch

To demonstrate performance implications, you can simulate a slow data fetch:

```typescript
// /app/lib/data.ts
export async function fetchRevenue() {
  try {
    // Artificial delay for demo purposes
    // Don't do this in production :)
    console.log("Fetching revenue data...");
    await new Promise((resolve) => setTimeout(resolve, 3000));

    const data = await sql<Revenue>`SELECT * FROM revenue`;
    console.log("Data fetch completed after 3 seconds.");
    return data.rows;
  } catch (error) {
    console.error("Database Error:", error);
    throw new Error("Failed to fetch revenue data.");
  }
}
```

### Testing the Delay

1. Open http://localhost:3000/dashboard/ in a new tab
2. Observe the delayed page load
3. Check terminal messages:
   ```
   Fetching revenue data...
   Data fetch completed after 3 seconds.
   ```

### Key Challenge

With dynamic rendering, your application's performance is constrained by your slowest data fetch.
