# Next.js Font and Image Optimization

## Font Optimization

### Using next/font

```tsx
import { Inter } from "next/font/google";

const inter = Inter({
  subsets: ["latin"],
});
```

### Key Features

- Zero layout shift
- Built-in performance
- Automatic self-hosting
- Custom fonts support

### Implementation

1. Create `fonts.ts` in UI folder
2. Import fonts from next/font/google
3. Apply in layout:

```tsx
<body className={`${inter.className} antialiased`}>
```

## Image Optimization

### Using next/image

```tsx
import Image from "next/image";

<Image src="/image.png" width={1000} height={760} alt="Description" />;
```

### Features

- Automatic optimization
- Lazy loading
- Prevents layout shift
- Responsive images
- Modern formats (WebP/AVIF)

### Best Practices

- Always specify width/height
- Use proper aspect ratios
- Place static images in `/public`
- Include descriptive alt text
- Use responsive classes:

```tsx
className = "hidden md:block"; // Desktop only
className = "block md:hidden"; // Mobile only
```

## Performance Benefits

- Reduced layout shift
- Optimized loading
- Better Core Web Vitals
- Improved SEO performance
