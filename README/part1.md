## 1. What is Next.js and Why Learn It

Next.js is a React framework that enables developers to build server-side rendered (SSR) and statically generated web applications with ease. It offers a range of features, including automatic code splitting, optimized performance, and a powerful routing system.

Learning Next.js is beneficial for several reasons:

- **Improved Performance**: Next.js optimizes your application for performance out of the box, ensuring fast load times and a smooth user experience.
- **SEO Benefits**: With server-side rendering, Next.js helps improve your application's search engine visibility.
- **Developer Experience**: Next.js provides a great developer experience with features like hot reloading, a rich plugin ecosystem, and easy deployment options.

## Server and Client Components

- **Server Components**:

  - By default, Next.js treats all components as Server components. These components can perform server-side tasks like reading files or fetching data directly from a database. The trade-off is that they can't use React hooks or handle user interactions.

- **Client Components**:
  - To create a Client component, you need to add the directive `"use client"` at the top of your component file. Client components can use React hooks and handle user interactions, but they can't perform server-side tasks. They are typically used for interactive parts of your application, such as forms or buttons. Client components are the traditional React components you're already familiar with from previous versions of React. They can use hooks and handle user interactions.

## 2. Installation
To install Next.js, you need to have Node.js and npm (Node Package Manager) installed on your machine. You can create a new Next.js project using the following command:

```bash
npx create-next-app@latest my-nextjs-app
cd my-nextjs-app
npm run dev
```
This will set up a new Next.js project and start the development server at `http://localhost:3000`.

## 3. Fundamental Concepts like RSC (React Server Components)
React Server Components (RSC) allow you to build components that run on the server, enabling better performance and reduced client-side JavaScript. In Next.js, you can create Server components by default, and you can also create Client components by adding the `"use client"` directive at the top of your component file.

## 4. Routing
  Routing conventions in Next.js are based on the file system. Here are the key conventions to follow:
   1. All routes must live inside the app folder.
   2. Route files must be named either page.js or page.tsx.
   3. Each folder represents a segment of the URL path.
  When these conventions are followed, the file automatically becomes available as a route.
   - Dynamic Routing
   - Nested Routing
   - Catch-All Routes

  ### 1. Dynamic Routing
 To create dynamic routes, you can use square brackets in your file names. For example, to create a dynamic route for user profiles, you can create a file named `[username]/page.js` inside the `app` folder. This will match any URL like `/john` or `/jane`.
  ### 2. Nested Routing
   Nested routing allows you to create routes within routes by organizing your folder structure accordingly. For example, if you have a blog with posts, you can create a folder structure like this:
   ```
   app
   └── blog
       ├── [slug]
       │   └── page.js
       └── page.js
   ```
   In this case, the `[slug]` folder represents a dynamic route for individual blog posts, while the `page.js` file inside the `blog` folder represents the main blog index page. URL paths like `/blog/my-first-post` will be handled by the `[slug]/page.js` file, while `/blog` will be handled by the `blog/page.js` file.
  ### 3. Catch-All Routes
   Catch-all routes allow you to match multiple segments in a URL. You can create a catch-all route by using double square brackets in your file names. For example, to create a catch-all route for a documentation section, you can create a file named `[[...slug]]/page.js` inside the `app` folder. This will match URLs like `/docs`, `/docs/getting-started`, or `/docs/guides/advanced`.
   like this:
   ```
   app
   └── docs
       ├── [[...slug]]
       │   └── page.js
       └── page.js
   ```
## 5. File Not Found Handling
Next.js automatically handles 404 errors for routes that do not exist. You can customize the 404 page by creating a `not-found.js` file inside the `app` folder. This file will be rendered whenever a user navigates to a non-existent route.

## End of part1.md

