## 11. Params and SearchParams

For a given URL,
params is a promise that resolves to an object containing the dynamic route parameters (like id).
searchParams is a promise that resolves to an object containing the query parameters (like filters and sorting).

### Note:

While page.tsx has access to both params and searchParams, layout.tsx only has access to params.
example:

```tsx
// app/products/[id]/page.tsx
export default async function ProductPage({
  params,
  searchParams,
}: {
  params: { id: string };
  searchParams: { [key: string]: string | string[] | undefined };
}) {
  const { id } = await params;
  const { lang } = await searchParams;
  //   or use this way
  //  const { id } = use(params) but now must add 'use client' at the top of the file
  //  const { lang } = use(searchParams) but now must add 'use client' at the top of the file
  return (
    <div>
      <h1>Product ID: {id}</h1>
      <p>Language: {lang}</p>
    </div>
  );
}
```

In this example, params contains the dynamic route parameter id, and searchParams contains the query parameter lang.

## 12. Navigating Programmatically

Next.js provides several hooks and functions to navigate programmatically within your application.

### Using `useRouter()` Hook

The useRouter hook allows you to access the router object, which provides methods for navigation.
example:

```tsx
"use client";
import { useRouter } from "next/navigation";
export default function NavigateButton() {
  const router = useRouter();

  const handleClick = () => {
    router.push("/target-page");
  };

  return <button onClick={handleClick}>Go to Target Page</button>;
}
```

### Using `usePathname()` Hook

The usePathname hook allows you to get the current pathname, which can be useful for conditional navigation.
example:

```tsx
"use client";
import { usePathname, useRouter } from "next/navigation";

export default function CurrentPath() {
  const pathname = usePathname();

  return <div>Current Path: {pathname}</div>;
}
```

### Redirecting with `redirect()` Function

The redirect function allows you to perform a server-side redirect from within a server component or page.
example:

```tsx
import { redirect } from "next/navigation";

export default async function Page() {
  redirect("/target-page");
}
```

In this example, when the Page component is rendered, it will immediately redirect the user to /target-page.

## 13. templates

Templates in Next.js allow you to define reusable structures for your pages, enabling consistent layouts and designs across different parts of your application.
example:

```tsx
// app/dashboard/template.tsx
export default function DashboardTemplate({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <div className="dashboard-layout"></div>
      <header>Dashboard Header</header>
      <main>{children}</main>
    </div>
  );
}
```

In this example, the DashboardTemplate component defines a layout structure with a header and a main content area. Any page that uses this template will have the same layout.

### Layout vs Template

### 1. Layout

- A layout is used to define a shared structure or UI wrapper that stays the same across multiple pages.
- It is rendered only once and does not re-render when you navigate between child pages.
- Layouts are persistent, meaning they keep their state, scroll position, and components (like a sidebar or header) when you move between routes.
- You usually use layouts for things like navigation bars, side menus, or page wrappers.

### 2. Template

- A template is similar to a layout but it re-renders every time you navigate to a new route.
- It is used when you want a new instance of the UI for each page — for example, when page transitions or animations are needed.
- Templates do not preserve state between route changes.

### Key Differences

Feature layout template
Re-render on navigation ❌ No ✅ Yes
State persistence ✅ Keeps state ❌ Loses state
Use case Shared UI (e.g., navbar, footer) Page transitions, animations
Performance Faster Slightly slower (more rebuilds)

layout → Persistent wrapper shared between pages.

template → Re-rendered wrapper for new page instances.

## 14. Error Handling

Next.js provides robust error handling mechanisms to manage errors gracefully in your application.

### Error Messages and Reset

You can create error boundaries to catch errors in specific parts of your application and display custom error messages.
example:

```tsx
"use client";
import { useState } from "react";

export default function ErrorBoundaryExample() {
  const [hasError, setHasError] = useState(false);

  const throwError = () => {
    setHasError(true);
  };

  if (hasError) {
    throw new Error("Something went wrong!");
  }

  return (
    <div>
      <h1>No Errors Yet</h1>
      <button onClick={throwError}>Throw Error</button>
    </div>
  );
}
```

### Error Boundaries

You can create error boundary components to catch JavaScript errors anywhere in their child component tree, log those errors, and display a fallback UI.
example:

```tsx
// app/error-boundary.tsx
'use client';
import { Component, ReactNode } from 'react';
interface ErrorBoundaryProps {
  children: ReactNode;
}
interface ErrorBoundaryState {
  hasError: boolean;
}
export default class ErrorBoundary extends Component<
  ErrorBoundaryProps,
  ErrorBoundaryState
> {
  constructor(props: ErrorBoundaryProps) {
    super(props);
    this.state = { hasError: false };
  }
    static getDerivedStateFromError() {
    return { hasError: true };
  }

  componentDidCatch(error: Error, errorInfo: React.ErrorInfo) {
    console.error('Error caught by ErrorBoundary:', error, errorInfo);
  }
    render() {
        if (this.state.hasError) {
        return <h1>Something went wrong.</h1>;
        }
        return this.props.children;
      }
}
```
## Global Error Handling
Next.js allows you to define a global error handling mechanism by creating a special error.js file in your app directory. This file will catch unhandled errors and display a custom error page.example:
```tsx
// app/error.js
export default function GlobalError() {
  return (
    <div>
      <h1>Oops! An unexpected error occurred.</h1>
      <p>Please try again later.</p>
    </div>
  );
}
```
In this example, any unhandled errors in your application will render the GlobalError component, providing a consistent error experience for users.
