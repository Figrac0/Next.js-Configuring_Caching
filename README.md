# Next.js 13 (Pre-Rendering_Data-Fetching_Optimizing)

## 🌟 Features

- **Server-Side & Client-Side Data Fetching**: Hybrid data loading strategies
- **Static & Dynamic Rendering**: Optimized pre-rendering with incremental static regeneration
- **Image Optimization**: Automatic image optimization using Next.js Image component
- **SEO Optimized**: Proper meta tags and structured data
- **Responsive Design**: Mobile-first responsive layout
- **Filtering System**: Advanced event filtering by date and location
- **Performance Optimized**: Fast page loads with optimized assets

## Project Overview


<p align="center">
  <img src="https://github.com/Figrac0/Next.js-Configuring_Caching_and_Advanced_Optimization/blob/DataF-Optimizing-Next13/public/1.png" alt="main photo" width="400"/><br/>
</p>

---

## 🚀 Key Technical Concepts Implemented

### 1. Pre-Rendering & Data Fetching Strategies

This project implements multiple Next.js data fetching patterns:

#### Static Site Generation (SSG) with `getStaticProps`
Used for pages with data that doesn't change frequently:
```javascript
export async function getStaticProps() {
    const featuredEvents = await getFeaturedEvents();
    return {
        props: { events: featuredEvents },
        revalidate: 1800, // Incremental Static Regeneration every 30 minutes
    };
}
```

## Dynamic Paths with getStaticPaths
For dynamic routes with fallback strategies:

```javascript
export async function getStaticPaths() {
    const events = await getFeaturedEvents();
    const paths = events.map((event) => ({ params: { eventId: event.id } }));
    return {
        paths: paths,
        fallback: "blocking", // Better UX with "blocking" fallback
    };
}
```

## Server-Side Rendering (SSR) with getServerSideProps
Commented but available for real-time data fetching:

```javascript
// export async function getServerSideProps(context) {
//   const filteredEvents = await getFilteredEvents({
//     year: numYear,
//     month: numMonth,
//   });
//   return { props: { events: filteredEvents } };
// }
```

## Client-Side Data Fetching with SWR
For dynamic filtering and real-time updates:

```javascript
const { data, error } = useSWR(
    "https://nextjs-course-c81cc-default-rtdb.firebaseio.com/events.json",
    (url) => fetch(url).then((res) => res.json()),
);
```

**Learn More**: [Next.js Data Fetching Documentation](https://nextjs.org/docs/pages/building-your-application/data-fetching)

## 2. Optimization Techniques

### Image Optimization
Using Next.js Image component for automatic optimization:

```jsx
<Image 
    src={`/${image}`} 
    alt={imageAlt} 
    width={300} 
    height={300}
    // Automatic features:
    // - WebP format conversion
    // - Lazy loading
    // - Responsive sizing
    // - CDN optimization
/>
```

### SEO Optimization with Next/Head
Page-level and app-level meta tag management:

```jsx
// Page-level meta tags
<Head>
    <title>NextJS Events</title>
    <meta name="description" content="Find a lot of great events..." />
</Head>

// App-level meta tags in _app.js
<Head>
    <meta name="viewport" content="initial-scale=1.0 width=device-width" />
</Head>
```

### Document-Level Customization
Custom `_document.js` for HTML structure optimization:

```javascript
import Document, { Html, Head, Main, NextScript } from "next/document";

class MyDocument extends Document {
    render() {
        return (
            <Html lang="en">
                <Head />
                <body>
                    <div id="overlays" />
                    <Main />
                    <NextScript />
                </body>
            </Html>
        );
    }
}
```

**Learn More**: [Next.js Optimization Documentation](https://nextjs.org/docs/pages/getting-started/images)

## 3. Performance Patterns

### Incremental Static Regeneration (ISR)
Combines static generation with periodic updates:

```javascript
revalidate: 1800 // Re-generate page every 30 minutes if requested
```

### Hybrid Rendering Strategy
- Static pages for event listings
- Dynamic rendering for filtered results
- Client-side fetching for interactive features

### Code Splitting & Lazy Loading
Automatic code splitting by Next.js Page Router
Component-level optimization with dynamic imports available

**Learn More**: [Next.js Performance Documentation](https://nextjs.org/docs/pages/building-your-application/optimizing/performance)

## 4. API Integration Patterns

### Centralized API Utilities
```javascript
export async function getAllEvents() {
    const response = await fetch(
        "https://next-13-datafetching-default-rtdb.firebaseio.com/Events.json",
    );
    const data = await response.json();
    
    const events = [];
    for (const key in data) {
        events.push({ id: key, ...data[key] });
    }
    return events;
}
```

### Error Handling Strategies
- Server-side validation in data fetching functions
- Client-side error boundaries
- Graceful degradation patterns

## 📁 Project Structure
```text
project/
├── components/
│ ├── events/ # Event-related components
│ ├── ui/ # Reusable UI components
│ └── layout/ # Layout components
├── helpers/
│ └── api-util.js # API utility functions
├── pages/
│ ├── events/ # Event pages
│ ├── _app.js # Custom App component
│ └── _document.js # Custom Document component
├── public/ # Static assets
└── styles/ # Global styles
```

## 🛠️ Built With

- **Next.js 13** - React framework with hybrid rendering
- **React 18** - UI library with concurrent features
- **CSS Modules** - Scoped styling solution
- **SWR** - React hooks for data fetching
- **Firebase Realtime Database** - Backend data storage


## 📚 Learning Resources

1. [Next.js Official Documentation](https://nextjs.org/docs)
2. [Data Fetching Patterns in Next.js](https://nextjs.org/docs/pages/building-your-application/data-fetching)
3. [Optimization Techniques](https://nextjs.org/docs/pages/building-your-application/optimizing)
4. [Page Router vs App Router](https://nextjs.org/docs/pages/building-your-application/routing)

## 🔗 Useful Links

- [Next.js GitHub](https://github.com/vercel/next.js)
- [React Documentation](https://reactjs.org/docs/getting-started.html)
- [Vercel Platform](https://vercel.com/docs)

## 🤝 Contributing

This project is for educational purposes demonstrating Next.js 13 patterns. While not actively maintained for production, it serves as a reference implementation for:
- Data fetching strategies
- Rendering optimization
- Performance best practices
- Next.js Page Router patterns
