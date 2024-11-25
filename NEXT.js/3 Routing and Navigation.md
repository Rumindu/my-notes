# Routing Overview

- In Next.js, routing is built upon the file system, simplifying the process of defining routes. Each folder inside the `app` directory represents a URL segment. For instance, creating a folder `users/new` will generate the URL `/users/new`. To expose a route publicly, a special file called `page.tsx` must be placed inside that folder. This `page` file renders the public-facing content.

- ## Key Features of the Next.js Router:
- **Special Files**: Next.js routing looks for certain key files:
    - **`page.tsx`**: The main file for rendering the page.
    - **`layout.tsx`**: Defines a common layout for pages.
    - **`loading.tsx`**: Used for displaying loading indicators.
    - **`route.ts`**: Handles API routes.
    - **`not-found.tsx` and `error.tsx`**: Custom error and 404 pages.

- Other files like CSS or JavaScript added to these folders, unless explicitly configured, won’t be exposed to the browser. They can be used internally without public access.

- ### Organizing Components in Next.js:
- As projects grow, complexity increases. Instead of dumping components into a general components folder, Next.js encourages **co-locating components with their associated pages**. For instance, in a `users` folder, the `UserTable.tsx` component can be added to keep things organized and avoid a messy centralized components folder.
- ### Example:
  1. **Create a `UserTable.tsx` component** inside the `users` folder.
  2. Move the logic (e.g., fetching users) from the `page.tsx` into the `UserTable.tsx` component.
  3. Insert the `UserTable` component inside the main page under a heading.
  4. [Source code](https://github.com/Rumindu/next-app/tree/4b8212f39c9fb0ee4b42f7e96803738a44525dfd/app/users)
- By organizing files in this manner, the app remains scalable, and components can later be moved to a general components folder if needed elsewhere in the app. This method improves maintainability as the project grows.
---

# Dynamic Routes
- In Next.js, dynamic routing allows you to create routes with parameters, enabling you to handle URL segments that change dynamically. This feature is essential when building pages that display specific resources, like user profiles or product details.

- ## Creating a Dynamic Route:
- To create a dynamic route, you need to define a folder in your `app` or `pages` directory with a parameter wrapped in square brackets (`[paramName]`). For example, in a `users` folder, you could create `[id]` to handle routes like `/users/1`.
- ### Example:
  1. **Create the Dynamic Route**:
     - In the `users` folder, create a subfolder called `[id]`.
     - Inside the `[id]` folder, create a `page.tsx` (or `page.js`).
  - **This structure would handle dynamic URLs like `/users/1` or `/users/2`.**
    
  2. **Accessing Route Parameters**:
     - Inside your dynamic page, access route parameters using the `props` object. You define an interface in TypeScript for the `props`, which will include a `params` object. For example:
      ``` tsx
      // app/users/[id]/page.tsx
      interface Props {
        params: { id: number };
      }
      // ...
      ```
    
     - You can destructure `params` to retrieve the dynamic parameter (`id`) and render it in your page:
      ``` tsx
      // app/users/[id]/page.tsx
      // ... 
	    // first de-structure params then de-structure it more and grab id
      const UserDetailPage = ({ params: { id } }: Props) => {
        return <div>UserDetailPage {id}</div>;
      };
      //For Below approach no need to define separate interface for props. 
      //It is done on inline
      //const UserDetailPage = ({ params: { id } }:{ params: { id: string } }) => {...
      ```
      [source code](https://github.com/Rumindu/next-app/blob/c9fdbd28bae8f8a216d17a115cde3bfbcca6e5f7/app/users/%5Bid%5D/page.tsx)
    
  3. **Nested Dynamic Routes**: You can also create nested dynamic routes, like `/users/1/photos/2`. This requires creating nested folders for each dynamic parameter.
    
    - Inside `[id]`, create another folder called `photos/[photoId]`.
    - In the `photos/[photoId]` folder, create a `page.tsx`.
    - The route will then have two dynamic parameters: `id` and `photoId`.
  
  4. **Handling Multiple Parameters**: Define both `id` and `photoId` in the `props` interface:
      ``` tsx 
      // app/users/[id]/photos/[photoId]
      interface Props {
        params: { id: number; photoId: number };
      }
      ```  
     - You can access and render both values:
        ``` tsx 
        // app/users/[id]/photos/[photoId]
        const PhotoPage = ({ params: { id, photoId } }: Props) => {
          return (
            <div>
              PhotoPage {id} {photoId}
            </div>
          );
        };
        ```
        [source code](https://github.com/Rumindu/next-app/blob/c9fdbd28bae8f8a216d17a115cde3bfbcca6e5f7/app/users/%5Bid%5D/photos/%5BphotoId%5D/page.tsx)
- ## Important Considerations:
- **Prop Drilling**: If a nested component on a page needs access to route parameters (like `id`), you must pass those parameters down from the page level to the component as props.
- **Reusable Components**: When parameters like `id` are needed in multiple places, you can move components into a shared folder once they become reusable across different routes.
---
# Dynamic Routes with Varying Parameters (catch-all route)

- In Next.js, you can create routes with a varying number of parameters using dynamic segments. This is useful for pages where the number of URL segments can change based on context, such as filtering products by categories or subcategories.

- ## Creating a Route with Varying Parameters 

- A **segment** refers to a portion of a URL path, separated by slashes (/). To handle dynamic segments, you don't need to create deeply nested folders for each parameter. Instead, Next.js offers a way to accept multiple parameters using the **catch-all route** syntax (`[...slug]`). Here's how to implement it:

- ## Example Workflow:

1. **Create the Folder Structure**:
    
    - In your `app` folder, create a folder named `products`.
    - Inside the `products` folder, create a dynamic route folder `[...slug]`.
    - This folder will now accept a flexible number of parameters, such as `/products/grocery`, `/products/grocery/dairy`, or `/products/grocery/dairy/milk`.
  
2. **Creating the Page Component**:
    
   - Inside the `[...slug]` folder, create a `page.tsx` file (or `page.js`).
   - In this page component, define the props interface with `slug` as an array of strings (`string[]`). This allows the route to capture multiple parameters:
    
    ``` tsx 
    // app/products/[...slug]/page.tsx
    interface Props {
      params: { slug: string[] }
    }
    ```
    
3. **Rendering Dynamic Slugs**:
    
   - The captured URL segments will be stored as an array of strings. You can render these segments to display or use them for filtering:
    
    ``` tsx
    // app/products/[...slug]/page.tsx
    const ProductPage = ({ params: { slug } }: Props) => {
      return (
        //use array's join method for clear output
        <div>Products/{slug.join('/')}</div>
      )
    }
    ```
    [source code](https://github.com/Rumindu/next-app/blob/34e80337f6b8a0910efa33fd58984f8a440dab42/app/products/%5B...slug%5D/page.tsx)

4. **Optional Route Parameters**: By default`[...slug]`, if you **visit `/products`, you'll get a 404 error** because the route requires at least one parameter. To make the parameter optional, rename the dynamic folder to `[[...slug]]`. This allows the route to work both with and without parameters:
    
    - `/products` (displays all products)
    - `/products/grocery` (displays grocery products)
    - `/products/grocery/dairy/milk` (displays filtered products)
    - [source code of my example](https://github.com/Rumindu/next-app/blob/1c95476a1edded9858275ff2074adf27e44a0d70/app/products/%5B%5B...slug%5D%5D/page.tsx)and [source code of Mosh example](https://github.com/mosh-hamedani/next-course/blob/2b711bf696df07b9750828b44a37832f09503011/app/products/%5B%5B...slug%5D%5D/page.tsx)

- ## Key Points:
  - **Catch-All Routes**: Using `[...slug]`, Next.js will capture any number of URL segments, making it easier to manage dynamic routes.
  - **Optional Parameters**: To allow optional parameters, use `[[...slug]]`, which makes it possible to access the route with or without parameters.
  - **Array of Parameters**: The `slug` parameter is an array, so you can handle multiple segments dynamically in your page.

- This approach is efficient for building flexible routes, especially when you want to filter or display content based on different URL parameters.
---

# Accessing Query String Parameters in Next.js

- In Next.js, query string parameters allow you to pass additional data in the URL that can affect how a page is rendered. Here's how you can access and use these parameters on the server side in Next.js.

- ## 1. Defining Query String Parameters:

- A query string is the part of a URL that comes after a `?` and allows for dynamic data to be passed. For example, a URL like `/products?sortOrder=price` has a query string parameter `sortOrder` with the value `price`.

- ## 2. Accessing Query String Parameters:

- In Next.js, query parameters are accessed using the `searchParams` property in the `props`. Here’s how to access and use them:

- **Step 1**: Define the `searchParams` property in the interface for `props`:

  ``` tsx 
  // app/products/[[...slug]]/page.tsx
  interface Props {
    params: { slug: string[] };
    searchParams: { sortOrder: string };
  }
  ```

- **Step 2**: Destructor the `searchParams` from the `props` in your page component:

  ``` tsx 
  // app/products/[[...slug]]/page.tsx
  const ProductPage = ({
    params: { slug },
    searchParams: { sortOrder },
  }: Props) => {
    return (
      <div>
        ProductPage {slug} {sortOrder}
      </div>
    );
  };
  ```
  [source code](https://github.com/Rumindu/next-app/blob/6491a7b8a5785967ed77f2d0d5fb3ea64fea1d81/app/products/%5B%5B...slug%5D%5D/page.tsx)
  ![](assets/Pasted%20image%2020240925201248.png)

- ## Task: Implementing Sorting in a Users Table Using Query Parameters 
- ### Key steps:
- **1. Modifying the Table Headers for Client-Side Navigation with Query Strings**:
  - Replace the static text in the table headers (like "Name" and "Email") with clickable links.
  - When navigating between different sorts, you can use **Next.js `Link` component**, which ensures client-side navigation without a full page reload. Instead of using an anchor tag (`<a>`). When clicking the links, the `sortOrder` query string parameter will be updated.
    ```tsx 
    // app/users/UserTable.tsx
    <th>
      <Link href="/users?sortOrder=name">Name</Link>
    </th>
    <th>
      <Link href="/users?sortOrder=email">Email</Link>
    </th>
    ```

- **2. Accessing Query Parameters on the Page**:
  - Query string parameters cannot be accessed directly in components. You need to handle them at the page level.
  - On the **users page**, destructor the `searchParams` to extract the `sortOrder` parameter.
    ``` tsx 
    // app/users.page.tsx
    interface Props {
      searchParams: { sortOrder: string }
    }

    // first de-structure searchParams then de-structure it more and grab sortOrder
    const UsersPage = async ({ searchParams: { sortOrder } }: Props) => {
      //confirmation purposes only
      console.log("sort-order",sortOrder);
      // ...
    }
    ```
    [source code](https://github.com/Rumindu/next-app/blob/70222e9353e95933a5301bd2a1c02d5cbe664c5a/app/users/page.tsx)

- **3. Passing the `sortOrder` to Components**:
  - Once you've accessed the query string parameter (`sortOrder`), pass it down as a **prop** to the `UserTable` component.
    ``` tsx 
    // app/users.page.tsx
    <UserTable sortOrder={sortOrder} />
    ```
    [source code](https://github.com/Rumindu/next-app/blob/70222e9353e95933a5301bd2a1c02d5cbe664c5a/app/users/page.tsx)
    
- **4. Implementing Sorting Logic in the `UserTable`**:
  - In the `UserTable` component, define an interface for props that includes `sortOrder`.
  - Use a sorting library like `fast-sort` to sort the users array based on the `sortOrder` value (either by **name** or **email**).
    ``` tsx 
    // app/users/UserTable.tsx
    import { sort } from "fast-sort";
    import Link from "next/link";
    // ...

    interface Props {
      sortOrder: string;
    }

    const UserTable = async ({ sortOrder }: Props) => {
      // ...
      const sortedUsers = sort(users).asc(
        sortOrder === "email" ? (user) => user.email : (user) => user.name
      );

      return (
        // ...
            <tbody>
              {sortedUsers.map((user) => (
                <tr key={user.id}>
                  <td>{user.name}</td>
                  <td>{user.email}</td>
                </tr>
              ))}
            </tbody>
        //..
      );
    };
    ```
    [source code](https://github.com/Rumindu/next-app/blob/70222e9353e95933a5301bd2a1c02d5cbe664c5a/app/users/UserTable.tsx)

---


# Layouts in Next.js

- ## What is a Layout?
- A **layout** in Next.js is a **shared UI structure** that is used across multiple pages of an application. Layouts allow developers to define a consistent visual framework (like headers, footers, and navigation) that wraps around individual page's content. This makes it easier to maintain and organize large applications where multiple pages need common interface components.

- ## Root Layout
- **Purpose**: The root layout defines a **common UI** structure that is shared across all pages in a Next.js application. This includes elements like the `<html>`, `<body>`, and common components such as navigation bars or footers.
- In the root layout file (typically located in the `app/` folder), the layout renders `children`, which represents the content of individual pages that are loaded at runtime.
  [example for root layout](https://github.com/Rumindu/next-app/blob/b87253e82766d97cdcb9b8953332115a7ca61ada/app/layout.tsx)

- ## Nested Layouts
- **Nested layouts** allow for page-specific UI components. For example, if all **admin pages** need a specific sidebar, header, or layout, you can create a layout specific to the admin section.
- **How to Create as an example**:
    1. Inside the `app/` folder, create a new folder, e.g., `admin/`.
    2. In the `admin/` folder, add a `layout.tsx` file, which acts as the layout for all pages within the `admin/` folder.

- ## Defining the Admin Layout
- Create a React component named `AdminLayout` in `layout.tsx` that structures the admin layout.
- The layout receives `children` as props (representing the page content).
  ``` tsx 
  // layout component must get children as props
  interface Props { 
    children: ReactNode;
  }

  const AdminLayout = ({ children }: Props) => {
    return (
      <div className='flex'>
        {/* Admin pages sidebar */}
        <aside className='bg-slate-200 p-5 mr-5'>Admin Sidebar</aside>
        <div>{children}</div>{/* Admin pages*/}
      </div>
    )
  }
  ```
  [source code](https://github.com/Rumindu/next-app/blob/b87253e82766d97cdcb9b8953332115a7ca61ada/app/admin/layout.tsx)

- ## Adding Admin Pages
- To use the layout, create a new page in the `admin/` folder (e.g., `admin/page.tsx`).
- **All pages inside the `admin/` folder will inherit the admin layout with the sidebar**.
    [source code](https://github.com/Rumindu/next-app/blob/b87253e82766d97cdcb9b8953332115a7ca61ada/app/admin/page.tsx)

- ## Summary
- The **root layout** provides a universal UI structure for all pages, while **nested layouts** like the **admin layout** allow for custom UI sections tailored to specific areas (e.g., admin pages). By using layouts, you can maintain consistency and reuse UI components across multiple pages in Next.js applications.
## Add Navigation bar to all pages
- ### Goal:
- The objective is to add a **navigation bar** that appears on all pages of the application using the **root layout** in Next.js.

- ### Steps to Implement the Navigation Bar

1. **Placing the Navbar in Root Layout**  
- Since the navigation bar is common across all pages, we will implement it in the **root layout**. To keep the layout clean, the navigation bar should be extracted into a separate component.
    
2. **Creating the Navbar Component**
    
   - In the `app/` folder, create a file called `navbar.tsx`. This component will handle the UI for the navigation bar.
   - Inside the `navbar.tsx` component, you will use **Tailwind CSS** for styling and **Flexbox** for horizontal layout.
   - Example structure:
      ``` tsx 
      // app/NavBar.tsx
      import Link from "next/link";
      import React from "react";

      const NavBar = () => {
        return (
          <div className="flex bg-slate-200 p-3">
            <Link href="/" className="mr-5">
              Next.js
            </Link>
            <Link href="/users">Users</Link>
          </div>
        );
      };
      ```
      [source code](https://github.com/Rumindu/next-app/blob/6bc9788860facf0c318ef4d2687a5857bd2ace85/app/NavBar.tsx)

3. **Integrating the Navbar in Root Layout**
    
   - Go back to the `layout.tsx` (root layout).
   - Import the `Navbar` component.
   - Render the `Navbar` **before** rendering the `children` to ensure that it appears on all pages.
   - Example structure:
      ``` tsx 
      //app/layout.tsx
      export default function RootLayout({
        children,
      }: {
        children: React.ReactNode;
      }) {
        return (
          <html lang="en" data-theme="winter">
            <body className={inter.className}>
              <NavBar />
              {/* render pages in the main area that is more semantic html */}
              <main className="p-5">{children}</main>
            </body>
          </html>
        );
      }
      ```
      [source code](https://github.com/Rumindu/next-app/blob/6bc9788860facf0c318ef4d2687a5857bd2ace85/app/layout.tsx)
  
4. **Additional Styling with Tailwind CSS**
    
   - The navigation bar now exists across all pages, but we also need to ensure the **main content area** has padding.
   - Modify the `main` element in the root layout by adding a **padding of 5** (`p-5`) using Tailwind CSS.

5. **Customizing Global Styles**
    
   - To style **heading elements** like `<h1>`, override the default Tailwind base styles in your global stylesheet (`global.css`):
        
     - Use the **base layer** in Tailwind to define styles for tags like `h1`, `h2`, etc.
        ``` css 
        /*app/globals.css*/
        @layer base {
          /* apply tailwind classes for <h1> */
          h1 {
            @apply font-extrabold text-2xl mb-3;
          }
        }
        ```
        [source code](https://github.com/Rumindu/next-app/blob/6bc9788860facf0c318ef4d2687a5857bd2ace85/app/globals.css)

     - This ensures that all `<h1>` elements across the app have a consistent font size, weight, and margin.
---

# Key Concepts About Next.js `<Link>` Component
- There are 3 things know about `<Link>` component
#### 1. **Only download content of Target Page** 

- When navigating using the **Next.js Link component**, only the **content of the target page** is downloaded. For example, if you're on the homepage and navigate to the users page:
    - The browser **does not re-download** other files like CSS, JavaScript, or even the navigation bar.
    - Only the **user page content** is fetched, reducing the number of requests made to the server compared to a full-page refresh.
- This selective downloading improves the efficiency of navigation within Next.js applications.

#### 2. **Pre-fetching Links in the Viewport**

- Next.js **automatically pre-fetches** links that are visible in the viewport. This happens only in **the production environment**.
- By doing so, Next.js reduces loading time when a user clicks on a link by **loading parts of the next page in advance**. This improves user experience as pages are rendered faster.
- To observe this, you can run the application in **production mode** using: `npm run build npm start`
    
#### 3. **Client-side Caching**

- Next.js caches the content of the pages you've visited in the **client-side cache**. This means:
    - On subsequent visits to the same page, Next.js fetches the content directly from the cache rather than making a request to the backend.
    - This cache is **session-based** and is cleared when a full-page reload occurs. Once cleared, the next navigation to that page will require a new request to the backend.

### Practical Observations:

- When navigating to the user's page, you might see two identical requests due to **React's Strict Mode** in development. Strict Mode renders components twice to help with error detection and debugging, but this does not happen in production(`npm run build` then `npm start`).
    
- The **RSC** (React Server Component) query parameter is seen when fetching the content of a React Server Component, illustrating how Next.js manages server-side rendering and data fetching.
    
In summary, **Next.js Link component** optimizes navigation by selectively fetching content, pre-fetching links in the viewport, and caching page content to enhance user experience and performance.

---

# Programmatic Navigation in Next.js

- In Next.js, **programmatic navigation** allows us to redirect the user to a different page as a result of certain actions like clicking a button or submitting a form. This is especially useful when we want to handle navigation without relying on traditional links. Here’s how programmatic navigation works:

#### 1. **Basic Link Navigation**

- A simple link can be added to the page using the **Link component**. For instance, on the users' page, you might create a button that links to a form for creating a new user:
  ``` tsx 
  // app/users/page.tsx
  <Link href="/users/new" className="btn">
    New User
  </Link>
  ```
  [source code](https://github.com/Rumindu/next-app/blob/94b5f1af1f18194c5720383fd2c72478c73d61c9/app/users/page.tsx)

#### 2. **Programmatic Navigation for Forms**
- When users submit a form, you often want to navigate programmatically after handling events like clicking a button or submitting the form.
- Handling browser events such as form submissions requires the component to be a **client-side component**. To do this, use the `use client` directive at the top of the file.
- Use the `use client` directive at the top of the file to make the component client-side.
- In a client-side component, **you cannot use the <Link> component** for programmatic navigation triggered by a button or form submission.
- Instead, we use Next.js' router object to navigate programmatically via browser events like onClick. To implement programmatic navigation, use the useRouter hook from the next/navigation module:
  ``` tsx 
  // app/users/new/page.tsx
  "use client";
  //don't import useRoute from next/router library
  import { useRouter } from "next/navigation";
  import React from "react";

  const NewUsers = () => {
    const router = useRouter();
    return (
      // Navigate to the users' page after button click
      <button className="btn btn-primary" onClick={() => router.push("/users")}>
        Create
      </button>
    );
  };
  ```   
  [source code](https://github.com/Rumindu/next-app/blob/94b5f1af1f18194c5720383fd2c72478c73d61c9/app/users/new/page.tsx) 
- **Important**: Ensure that the router is imported from the correct module (`next/navigation`) in Next.js 13 and later. Importing from the older `next/router` module will cause errors in the app.

#### 3. **Executing Programmatic Navigation**

- When the button is clicked (or the form is submitted), the user is automatically redirected to the desired page (in this case, `/users`), using the `router.push()` method.
- This eliminates the need for manual redirects and creates a smoother user experience.

Programmatic navigation is essential when working with dynamic forms or actions that need conditional redirects, enabling more control over user interactions and navigation flow.

---

# Loading UI and Suspense in Next.js

1. **Suspense in React 18**:
    
   - Suspense allows showing a **fallback UI** (like a loading spinner) while a component is being rendered.
   - In Next.js, you can wrap components in `Suspense` to display a loading indicator while fetching data. Example usage:

      ``` tsx 
      // app/users/page.tsx
      import { Suspense } from "react";
      <Suspense fallback={<p>Loading...</p>}>
        <UserTable sortOrder={sortOrder} />
      </Suspense>
      ```
      [source code](https://github.com/Rumindu/next-app/blob/a7f29161f73565d9a4cb33822db39c1fc0b08304/app/users/page.tsx)
   - The `fallback` prop can be set to any UI element (e.g., plain text or a spinner component) displayed until the component finishes loading.
  
2. **React DevTools**:
    
   - In Chrome DevTools, after installing the **React DevTools extension**, you can inspect the Suspense component to see whether it is suspended.
   - click on marked icon to suspend `suspend component`.
    ![](assets/Pasted%20image%2020240926202036.png)
   - This tool is useful for testing what users will experience when waiting for data to load.
  
3. **Streaming in Next.js**:
    
   - When the server sends the page, it **streams HTML** to the client.
   - Initially, server send the fallback UI, but it doesn't close the connection. It doesn't terminate request response life cycle. Server will wait for the user table component to render. Once the data for the component (e.g., `UserTable`) is ready, the server sends the remaining data to the client. This is call **streaming**
   ![](assets/Pasted%20image%2020240927055013.png)
   - This ensures better **SEO** performance since search engine bots can see the entire page once the data is fully streamed.
  
4. **Global Suspense with Layout**:
    
   - To make sure every page shows a loading UI while navigating between pages, you can wrap the `children` in the root `layout.tsx` file inside a `Suspense` component:
    
      ``` tsx 
      // app/layout.tsx
      <Suspense fallback={<p>Loading ....</p>}>{children}</Suspense>
      ```
      [source code](https://github.com/Rumindu/next-app/blob/a9b204d443832f062fea28cf90b30df2ff23177f/app/layout.tsx)

5. **Special `loading.tsx` File**:

   - Instead of manually adding `Suspense` components, Next.js offers a simpler solution by creating a `loading.tsx` file in any folder under the `app/` directory.
   - This file automatically shows the loading UI when a page in the folder is being rendered.
      ``` tsx 
      // app/loading.tsx
      const loading = () => {
        return (
          <div>Loading .....</div>
        )
      }

      export default loading
      ```

6.  **Enhancing Loading UI with DaisyUI**:
    
    - You can make the loading UI more visually appealing by using **DaisyUI** components like spinners or loading animations.
    - Example of a spinner:
    
      ``` tsx 
      const Loading = () => {
        return (
          <span className="loading loading-spinner loading-md"></span>
        )
      }
      ```
      [source code](https://github.com/Rumindu/next-app/blob/83fcdc4b757cb40da8e4794c10bcf1cfd29e87bd/app/loading.tsx)
  
    - Visit [DaisyUI](https://daisyui.com/components/loading/) for more components like loading dots, rings, or balls.
---

# Handling "Not Found" Errors in Next.js

In Next.js, you can customize how 404 pages (Not Found errors) are displayed to users, offering both general and specific custom error pages.

1. **Default 404 Page**:
    
   - When a user navigates to a page that doesn't exist, Next.js serves a **default 404 page**. However, you can create a custom version of this page.

2. **Creating a Custom 404 Page**:
    
   - To customize the 404 page for your entire app, add a file called `not-found.tsx` in the `app/` folder.
   - In this file, export a React component that will render a custom message when a non-existent page is visited.
    
      ``` tsx 
      // app/not-found.tsx
      const NotFoundPage = () => {
        // reason for having "doesn&apos;t" instead of "doesn't" describe at below S.S. s
        return <div>The requested page doesn&apos;t exist.</div>;
      };

      export default NotFoundPage;
      ```
      [Source code](https://github.com/Rumindu/next-app/blob/94cc644df6a1a53f8bc2f5df49b882846a2efc70/app/not-found.tsx)
      ![](assets/Pasted%20image%2020240927091259.png)
      
      ![](assets/Pasted%20image%2020240927091409.png)
    
3. **Customizing Not Found Pages for Specific Routes**:
    
    - You can also create **custom 404 pages for specific routes** or sections of your app.
    - For example, in a user detail page (`/users/[id]`), you might want a more specific error message if the user ID doesn't exist.
    - In your route folder (e.g., `/users/[id]`), add another `not-found.tsx` file, which will handle "Not Found" errors for that specific route.
    
      ``` tsx 
      // app/user/[id]/not-found.tsx
      const UserNotFoundPage = () => {
        return (
          <div>This user doesn&apos;t exist.</div>
        )
      }
      ```
      [Source code](https://github.com/Rumindu/next-app/blob/94cc644df6a1a53f8bc2f5df49b882846a2efc70/app/users/%5Bid%5D/not-found.tsx)
    
4. **Programmatically Triggering 404 Errors**:
    
    - You can trigger a 404 error in specific situations by calling the **`notFound()` function** from the `next/navigation` package.
    - For example, if you're fetching a user by ID and the ID is greater than 10, you can trigger a 404:
    
      ```tsx
      // app/users/[id]/page.tsx
      import { notFound } from "next/navigation";

      interface Props {
        params: { id: number };
      }

      const UserDetailPage = ({ params: { id } }: Props) => {
        if (id > 10) notFound();
        return <div>UserDetailPage {id}</div>;
      };
      ```
      [source code](https://github.com/Rumindu/next-app/blob/94cc644df6a1a53f8bc2f5df49b882846a2efc70/app/users/%5Bid%5D/page.tsx)
---

# Handling Unexpected Errors in Next.js

- Next.js provides built-in mechanisms to handle unexpected errors and create custom error pages to enhance user experience. Here’s how you can handle errors effectively in your Next.js application:
- To ==simulate an unexpected error, you can introduce an invalid endpoint== or similar issues in your component. For example, in the [user table component](https://github.com/Rumindu/next-app/blob/987bf65be5d0336902a5ea7276f4af0a01b69357/app/users/UserTable.tsx), you can add an invalid endpoint to trigger an error.
    
    
1. **Default Development vs. Production Error Pages**:
    
   - In **development mode**, Next.js shows detailed error messages that help you debug the issue. You’ll see where the error occurred along with the stack trace.
   - In **production mode**, Next.js displays a generic error page, which can be customized.
  
2. **Creating a Custom Error Page**:
    
   - To create a custom error page, add an `error.tsx` file in the `app/` folder.
   - In this file, export a React component that will render when an error occurs. It’s important to make this a **client component** to handle user interactions like retrying.
      ``` tsx
      // reason for `error` is being client component is explained in point 7
      "use client";

      const ErrorPage = () => {
        return <div>An unexpected error has occurred.</div>;
      };
      ```
      [source code](https://github.com/Rumindu/next-app/blob/987bf65be5d0336902a5ea7276f4af0a01b69357/app/error.tsx)
    
3. **Custom Error Pages for Specific Routes**:
    
   - You can create custom error pages for specific sections of your app. For example, inside the `users/` folder, you can add an `error.tsx` file to handle errors specific to user-related routes.
   - In most cases, having a global error page is sufficient for catching all unexpected errors in the application.
  
4. **Handling Errors in the Root Layout**:
    
   - Errors that occur in the **root layout** cannot be caught by regular error pages. To handle errors in the layout, create a `global-error.tsx` file in the `app/` folder, which will act as a global error handler.

5. **Accessing the Error Object**:
    
   - Next.js automatically passes the error object to the error component. You can log this error to an external service like **Sentry** for persistence and debugging.
   - Use the `error` prop to access the error details
      ``` tsx 
      "use client";

      interface Props {
        error: Error;
      }
      const ErrorPage = ({ error }: Props) => {
        console.log("Error", error);
        return <div>An unexpected error has occurred.</div>;
      };
      ```
      [source code](https://github.com/Rumindu/next-app/blob/86a9388a6c58e4284a42c2e71a583881793f5b87/app/error.tsx)
  
6. **Retrying After an Error**:
    
   - Sometimes errors may be temporary, so it’s useful to provide a retry option. The `reset` function passed to the error component allows you to reset the error state and attempt the operation again.
   - Example of a retry button:
      ``` tsx 
      interface Props {
        error: Error;
        reset: () => void;
      }
      const ErrorPage = ({ error, reset }: Props) => {
        console.log("Error", error);
        return (
          <>
            <div>An unexpected error has occurred.</div>
             {/*reason for `error` is being client component*/}
            <button className="btn" onClick={() => reset()}>
              Retry
            </button>
          </>
        );
      };
      ```
        [source code](https://github.com/Rumindu/next-app/blob/2176ec9c2ee86fab4cf0e85b6f1ea771b5ba7d97/app/error.tsx)
7. **Caution with Retrying**:
    
   - Be careful when allowing retries, as it may lead to repetitive errors. Use the retry mechanism selectively in your app, where it makes sense to give users the option to retry.

8. **Logging Errors**:
    
   - It is a best practice to log errors to a service like **Sentry** or a similar logging platform. This way, you can track, analyze, and fix errors more efficiently in production environments.
