## 6. Private Folders
Private folders in Next.js are used to store components, utilities, or any code that should not be directly accessible via routing. These folders are typically prefixed with an underscore (_) or placed in a special directory to indicate their private nature.
Private folders are super useful for a bunch of things:
- Keeping your UI logic separate from routing logic.
- Having a consistent way to organize internal files in your project.
example:
```
my-nextjs-app/
├── app/
│   ├── _components/        # Private folder for reusable components
│   │   ├── Header.js
│   │   └── Footer.js
│   ├── page.js              # Public route
│   └── about/
│       └── page.js          # Public route
└── ...
```
In this example, the `_components` folder is private and contains reusable components like `Header` and `Footer`. These components can be imported and used in public route files like `page.js` and `about/page.js`, but they cannot be accessed directly via a URL.
To use components from a private folder, you would import them like this:
```javascript
import Header from '../_components/Header';
import Footer from '../_components/Footer';
function HomePage() {
  return (
    <div>
      <Header />
      <h1>Welcome to the Home Page</h1>
      <Footer />
    </div>
  );
}
export default HomePage;
```
By organizing your code this way, you can maintain a clean separation between your application's internal logic and its public-facing routes.

## 7. Route Groups
Route groups in Next.js allow you to organize your routes into logical sections using named folders. This helps keep your project structure clean and makes it easier to manage related routes together.
To create a route group, you can use parentheses in folder names. For example, you might have an `(admin)` folder for admin-related routes and a `(user)` folder for user-related routes.
example:
```
my-nextjs-app/
├── app/
│   ├── (admin)/              # Route group for admin routes
│   │   ├── dashboard/
│   │   │   └── page.js        # /admin/dashboard
│   │   └── settings/
│   │       └── page.js        # /admin/settings
│   ├── (user)/               # Route group for user routes
│   │   ├── profile/
│   │   │   └── page.js        # /user/profile
│   │   └── orders/
│   │       └── page.js        # /user/orders
│   └── page.js                # Public route
└── ...
```
In this example, the `(admin)` folder contains routes related to admin functionalities, while the `(user)` folder contains routes for user functionalities. Each route group can have its own nested routes.
To navigate to these routes, you would use the corresponding paths:
- `/admin/dashboard` for the admin dashboard.
- `/admin/settings` for admin settings.
- `/user/profile` for the user profile.
- `/user/orders` for user orders.
Using route groups helps you maintain a well-organized project structure, making it easier to manage and scale your Next.js application.

## 8. Layouts
Layouts in Next.js allow you to define a consistent structure for your pages. You can create multiple root layouts to provide different layouts for different sections of your application. Additionally, you can use layouts inside route groups to further customize the appearance and structure of specific sections.
### Multiple Root Layouts
You can create multiple root layouts by defining separate `layout.js` files in different folders. Each layout can have its own structure and styling.
example:
```my-nextjs-app/
├── app/
│   ├── layout.js              # Root layout for the entire app
│   ├── (admin)/              # Route group for admin routes
│   │   └── layout.js          # Layout specific to admin routes
│   ├── (user)/               # Route group for user routes
│   │   └── layout.js          # Layout specific to user routes
│   └── page.js                # Public route
└── ...
```
In this example, the root `layout.js` defines the overall structure for the app, while the `(admin)/layout.js` and `(user)/layout.js` provide specific layouts for their respective route groups.

## 9. Metadata
Metadata in Next.js allows you to manage information about your web pages, such as titles, descriptions, and other meta tags. This is important for SEO and improving the user experience. You can export a static metadata object or a dynamic `generateMetadata` function to manage your page metadata.
example of static metadata:
```javascript
// app/page.js
export const metadata = {
  title: 'Home Page',
  description: 'Welcome to the home page of our Next.js application.',
};
```
example of dynamic metadata:
```javascript
// app/product/[id]/page.js
export async function generateMetadata({ params }) {
  const product = await fetchProductById(params.id);
  return {
    title: product.name,
    description: product.description,
  };
}
```
In this example, the `generateMetadata` function fetches product data based on the dynamic route parameter `id` and returns metadata specific to that product.
By managing metadata effectively, you can enhance your application's SEO and provide relevant information to users and search engines.
### Supported Metadata Fields

- `title`: The title attribute is used to set the title of the document. It can be defined as a simple string or an optional template object.
example:
```javascript
export const metadata = {
  title: 'My Next.js App',
};
```
or with a template:
```javascript
export const metadata = {
  title: {
    default: 'My Next.js App',
    template: '%s | My Next.js App',
  },
};
```
title template can be used to add a prefix or a suffix to titles defined in child route segments.
For example, if you have a child route with the title "Dashboard", the template will render the full title as "Dashboard | My Next.js App".
title absolute can also be used to set a fixed title that does not follow the template.
example:
```javascript
export const metadata = {
  title: {
    absolute: 'Fixed Title',
  },
};
```
In this case, the title will always be "Fixed Title", regardless of any templates or child route titles.

## 10. Navigation
Navigation in Next.js is essential for creating a seamless user experience in your web application. Next.js provides several tools and components to help you navigate between pages and manage routing effectively.
### Link Components
The `Link` component from `next/link` is used to create client-side navigation between pages. It enables faster transitions and prefetching of linked pages.
example:
```javascript
import Link from 'next/link';
function HomePage() {
  return (
    <div>
      <h1>Welcome to the Home Page</h1>
      <Link href="/about">Go to About Page</Link>
    </div>
  );
}
export default HomePage;
```
### Replace Navigation
You can use the `replace` prop in the `Link` component to replace the current history entry instead of adding a new one. This is useful for scenarios like login redirects.
example:
```javascript<Link href="/dashboard" replace>Go to Dashboard</Link>
```
### Active Link Detection using `usePathname()`
The `usePathname` hook from `next/navigation` allows you to get the current pathname, which can be useful for highlighting active links in your navigation.
example:
```javascriptimport { usePathname } from 'next/navigation';
import Link from 'next/link';
function Navbar() {
  const pathname = usePathname();
  return (
    <nav>
      <Link href="/" className={pathname === '/' ? 'active' : ''}>Home</Link>
      <Link href="/about" className={pathname === '/about' ? 'active' : ''}>About</Link>
    </nav>
  );
}
export default Navbar;
```
## End part2.md
