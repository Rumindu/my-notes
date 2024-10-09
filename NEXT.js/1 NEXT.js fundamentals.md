# Introduction
- NEXT.js is a framework for building super fast and search engine friendly applications which built on top of React.
- React is just a library for creating interactive UIs but NEXT.js is a comprehensive framework.
- Framework is a collection of libraries, tools and conventions that streamline application development.
- As an example NEXT.js include its own routing library. So we don't need to use a separate library like React Route.
- Using Next.js we can also do full stack development.
---

# Initiate NEXT.js project
- `npx create-next-app@latest` to create latest version NEXT.js project
- Here we specifically using `v13.4.13` so that we run `npx create-next-app@13.4.13`
- After that we need to give a project name and all configuration options value set as default. 
---
# Project Structure
```  
next-app
    │   .eslintrc.json
    │   .gitignore
    │   next-env.d.ts
    │   next.config.js
    │   package-lock.json
    │   package.json
    │   postcss.config.js
    │   README.md
    │   tailwind.config.ts
    │   tsconfig.json
    │
    ├───app //container for routing system
    │       favicon.ico
    │       globals.css
    │       layout.tsx
    │       page.tsx
    │
    └───public
            next.svg
            vercel.svg

```
[Source code](https://github.com/Rumindu/next-app/tree/de48934fd9e7aff26e2c5f5aefc6cf6d3a9a9094)

---

# Routing
- Routing in the NEXT.js is based on the file system.
- As an example created a new folder called `users`. For publicly accessible here we should add `page.tsx` file 
  ```
  App
  │   layout.tsx
  │   page.tsx
  │   
  └───users
          page.tsx
  ```
- Make sure to name this file correctly. ==page in lower case==.
- Because this is one of the convention NEXT.js is looking for. Otherwise routing won't work.
- `page.tsx` exports a React component that will render when types "/users" at the address bar.
  ``` tsx 
  // users/page.tsx
  import React from 'react'

  //The name we assign here doesn't really matter in terms of routing,
  //this is just for better organization of our code
  const UsersPage = () => {
    return (
      <div> UsersPage</div>
    )
  }

  export default UsersPage
  ```
  [Source code](https://github.com/Rumindu/next-app/tree/66b06a4247774bea66e590acf205532bae01b2a1/app)
  ![](assets/Pasted%20image%2020240915175001.png)
- If we add another file in to `users` folder like `test.css` and try to access using "users/test.css" we get not found page.
  ```
  App
  └───users
          page.tsx
          test.css
  ```
  ![](assets/Pasted%20image%2020240915175355.png)
- So this is how the new ==App router== is differ from old Page router. In the page router if we put any file in side `users` folder those file would be publicly accessible.
## Nested routes
```
App
│   layout.tsx
│   page.tsx
│
└───users
    │   page.tsx
    │
    └───new
            page.tsx
```

``` tsx 
// users/new/page.tsx
import React from 'react'

const NewUsers = () => {
  return (
    <div>NewUsers</div>
  )
}

export default NewUsers
```
[Source code](https://github.com/Rumindu/next-app/tree/c207372d24d22860e82fa8d1fd479bbe14304bd0/app/users/new)

![](assets/Pasted%20image%2020240915180700.png)
---
# Navigation
- We can use anchor tag for navigation. But it isn't optimal way. optimal way is using `<Link>` component in `next/link` library.
``` tsx 
// pages.tsx
import Link from 'next/link'

export default function Home() {
  return (
    <main><h1>Hello World</h1>
    <Link href="/users">users</Link>
    </main>
  )
}
```
[Source code](https://github.com/Rumindu/next-app/blob/7a088608f7084dcfc6a495aebe0cc31a2e786cf9/app/page.tsx)

---

# Client and Server component

- In a Next.js project, components can be rendered in 2 different environments:
  - **Client-side Rendering (CSR)**: Components are rendered on the client within a web browser, similar to how React applications work.
  - **Server-side Rendering (SSR)**: Components are rendered on the server, typically within a Node.js runtime.
- In CSR, all components are bundled and sent to the client for rendering.
- The bundle size increases as the application grows in complexity.
- **Issues with CSR**:
    - Larger bundles result in higher memory usage on the client.
    - Therefore client needs more resources
    - Search engine bots cannot index the content since they cannot execute JavaScript.
    - Sensitive data, such as API keys, may be exposed to the client.
- With SSR, components are rendered on the server and only essential HTML markup is sent to the client.
- **Benefits of SSR**:
    - Reduced bundle size, as fewer components are sent to the client.
    - Requires fewer client resources for rendering.
    - Search engine bots can index the content, improving SEO.
    - Sensitive data can be kept on the server, enhancing security.

- In SSR, the content is rendered on the server, and a fully-rendered HTML document is sent to the client. This improves SEO as search engine bots can crawl and index the content.

- Server-rendered components lack **interactivity**:
  - They cannot listen to browser events like `click`, `change`, or `submit`.
  - They cannot access browser-specific APIs such as `localStorage`.
  - They cannot maintain state or use React hooks like `useEffect`.

- In real-world applications, we often use a mix of **client** and **server** components:
  - **Default to server components** for rendering as much content as possible on the server.
  - Use **client components** only when interactivity is needed.

- ### Example: Product Page with SSR and CSR

- Let’s imagine you want to build a product page that displays several components like `NavBar`, `Sidebar`, `ProductList`, `ProductCard`, `Pagination`, and `Footer`.
- In traditional React applications (CSR), all these components are bundled and sent to the client.
- In Next.js, we can render all non-interactive components on the server and minimize the bundle size.
- Extracting a Client Component
  - For instance, to add a product to a shopping cart, we need a button that handles user interaction. This can be separated into a **client component**, while keeping the rest of the content server-rendered.

- #### Code Example: Server and Client Components
1. **`ProductCard`(Server Component)**:
  ```tsx
  // components/ProductCard.tsx
  import React from 'react'
  import AddToCart from './AddToCart';

  const ProductCard = () => {
    return (
      <div>
        <AddToCart />
      </div>
    )
  }

  export default ProductCard;
  ```

2. `AddToCart` (Client Component)**:
  ``` tsx
  // components/AddToCart.tsx
  'use client'; // This directive makes it a client component
  import React from 'react'

  const AddToCart = () => {
    return (
      <div>
        <button onClick={() => console.log('Click')}>Add to Cart</button>
      </div>
    )
  }

  export default AddToCart;
  ```
  [Source code](https://github.com/Rumindu/next-app/tree/32a380e9d2077ca96d091275ea6de50a9488f17b/app/components)

- The `ProductCard` component is rendered on the **server**, reducing the bundle size and improving performance.
- The `AddToCart` is a **client component** that handles the `click` event, which allows for interactivity.
- In Next.js, all components inside the `app/` folder are **server components** by default.
- To enable interactivity, you can mark a component as a **client component** by adding the `'use client'` directive at the top of the file.

- Difference Between `app/` router and `pages/` router
  - The **app/** router supports both server and client components, making it the preferred approach for new Next.js projects.
  - The **pages/** router (legacy routing system) does not support server components. For future development, it's recommended to switch to the new app router.

- ### Summary of CSR vs SSR

|Feature|Client-side Rendering (CSR)|Server-side Rendering (SSR)|
|---|---|---|
|**Rendering Location**|Client (browser)|Server (Node.js runtime)|
|**Bundle Size**|Increases with app complexity|Smaller since only essential components are sent|
|**Search Engine Optimization**|Difficult (bots can't execute JavaScript)|Easier (content is pre-rendered on the server)|
|**Sensitive Data Protection**|Exposed on the client|Kept secure on the server|
|**Interactivity**|Full interactivity (event listeners, state)|Limited (no event handling, access to browser APIs)|
|**Use Case**|When interactivity is needed|When static content or SEO is important|

- By balancing **CSR** and **SSR**, we can create fast, SEO-friendly, and secure applications in Next.js. In general, aim to render as much content as possible on the server and use client components only when necessary for interactivity.
---
# Data Fetching
- In Next.js, there are 2 main ways to fetch data: **on the client** or **on the server**. Each approach has its advantages and limitations. This guide explores both methods and demonstrates the best practices for fetching data in Next.js. Here we use [JSONPlaceholder](https://jsonplaceholder.typicode.com/)API end point to get dummy data
- To fetch data on the client side, we typically use React hooks like `useState` and `useEffect`. These hooks allow us to store data in state and fetch it from an API when the component mounts.
  ``` jsx
  'use client';
  import React, { useState, useEffect } from 'react';

  function Users() {
    const [users, setUsers] = useState([]);

    useEffect(() => {
    const fetchData = async () => {
      try {
        const response = await fetch('https://jsonplaceholder.typicode.com/users');
        const data = await response.json();
        setUsers(data);
      } catch (error) {
        console.error("Error fetching data:", error);
      }
    };

    fetchData();
  }, []);

    return (
      <div>
        <h1>Users</h1>
        <ul>
          {users.map(user => (
            <li key={user.id}>{user.name}</li>
          ))}
        </ul>
      </div>
    );
  }

  export default Users;
  ```
- Issues with Client-side Data Fetching
  - **Bundle Size**: As the application grows, more components are shipped to the client, increasing the bundle size.
  - **Performance**: The rendering happens entirely on the client, making the application resource-intensive.
  - **SEO**: Search engines cannot see the content immediately because data is fetched after the page loads, making it less search engine friendly.
  - **Security**: Sensitive information like API keys can be exposed to the client.
  - **Extra Round Trip**: The browser first downloads the HTML, CSS, and JavaScript files, then makes an additional request to fetch data, adding latency.
- By fetching data on the server, we can eliminate most of the problems associated with client-side fetching. In Next.js, server components make it easy to fetch data on the server without using state or effect hooks.
  ``` tsx
  // users/page.tsx

  //to improve the development experience with auto-complete suggestions.
  interface User {
    id: number;
    name: string;
  }

  const UsersPage = async () => {
    const res = await fetch("https://jsonplaceholder.typicode.com/users");
    //res is parsing to json formate
    const users: User[] = await res.json();
    return (
      <>
        <h1>Users</h1>
        <ul>
          {users.map((user) => (
            <li key={user.id}>{user.name}</li>
          ))}
        </ul>
      </>
    );
  };

  export default UsersPage;

  ```
- Benefits of Server-side Data Fetching
  - **Smaller Bundle**: Since the component is rendered on the server, less code is sent to the client, resulting in a smaller bundle.
  - **Improved Performance**: Rendering happens on the server, reducing the load on the client.
  - **SEO-friendly**: Search engine bots can crawl and index the content since it is pre-rendered on the server.
  - **Security**: Sensitive data like API keys can remain on the server, away from the client.
  - **No Extra Round Trip**: The data is fetched and rendered on the server, so the client receives the fully-rendered HTML in the initial request, avoiding extra round trips.

- Steps to Fetch Data on the Server
  1. **Use the `fetch` function**: This function is available on both the client and server. When used in server components, it performs the HTTP request on the server.
  2. **Mark the component `async`**: Since data fetching returns a promise, make the component asynchronous to use `await`.
  3. **Map the data**: Once the data is fetched, it can be mapped into HTML elements, just like in React applications.

- Comparing Client-side and Server-side Data Fetching

|Feature|Client-side Fetching|Server-side Fetching|
|---|---|---|
|**Rendering**|In the browser (after initial page load)|On the server (before sending HTML to the client)|
|**Bundle Size**|Larger (includes state management and fetch logic)|Smaller (data is fetched and rendered on the server)|
|**Performance**|Resource-intensive on the client|Offloads rendering to the server, reducing client load|
|**SEO**|Poor (content not visible to search engines initially)|Excellent (content is pre-rendered and visible to bots)|
|**Security**|Sensitive data exposed on the client|Sensitive data stays secure on the server|
|**Round Trip for Data Fetching**|Extra round trip to fetch data|No extra round trip (data fetched with initial request)|

- Whenever possible, it's recommended to fetch data in server components to:
  - **Improve SEO**: Content is pre-rendered, making it accessible to search engines.
  - **Reduce Bundle Size**: Server-rendered components minimize the amount of JavaScript sent to the client.
  - **Optimize Performance**: By offloading the rendering to the server, the client’s workload is reduced.
  - **Enhance Security**: Sensitive data such as API keys remain hidden from the client.
---
# Caching
- **Caching** is an important optimization in web development, especially in **Next.js**, where it's automatically built into server-side data fetching.
- Caching refers to the process of storing data in a location where it can be accessed more quickly than repeatedly fetching it from slower sources. Generally, there are three main places where data can be fetched from:
  1. **Memory** – Fastest access.
  2. **File System** – Slower than memory but faster than network requests.
  3. **Network** – Slowest access since it involves communication over the internet.
- In Next.js, data caching helps to avoid repeated, slow network requests by saving the data on the file system after the first request.
- Whenever we use the `fetch()` function in **Next.js** server components, the result is automatically cached by the framework. The data is stored in **Next.js’s data cache** (file system-based), so when you make the same request again, it retrieves the data from the cache instead of the network.
- This is particularly useful in scenarios where:
  - The data is static or doesn’t change frequently.
  - There is a need to reduce the number of network calls, improving performance.

- ### Controlling Caching Behavior

- Next.js provides full control over the caching behavior through the `fetch()` function. Here’s how you can customize caching:

1. **Disable Caching with `cache: 'no-store'`**:
    
   - This is useful when fetching data that changes frequently.
   - It ensures that the data is always fresh and not served from cache.
    
  ```tsx 
  const res = await fetch(
    'https://jsonplaceholder.typicode.com/users', 
    {cache: 'no-store'}
  );
  ```
  [Source code](https://github.com/Rumindu/next-app/tree/d220a4897af133099be716881706a762a21ea7a3)
    
    
2. **Revalidate Data with `next: { revalidate: X }`**:
    
   - This option allows you to cache the data but also re-fetch it in the background after a specific interval (e.g., 10 seconds).
   - This keeps the cached data fresh without forcing the user to wait for a new request every time.
    
  ``` tsx 
  const res = await fetch(
    'https://jsonplaceholder.typicode.com/users', 
    {next: { revalidate: 10 }}
  );
  ```
  [Source code](https://github.com/Rumindu/next-app/blob/0325eaa26e368de8c4408cee49dd26511861a379/app/users/page.tsx)
    
   - In this example, the data will be revalidated every 10 seconds, meaning a background job will update the cache with fresh data every 10 seconds.

- #### Important Points to Note:

- **Next.js’s built-in caching** is only available when using the native `fetch()` function.
- If you use third-party libraries like **Axios**, you won’t benefit from this automatic caching mechanism.
- For example, Axios does not cache data:
  ```jsx 
  const res = await axios.get('https://jsonplaceholder.typicode.com/users');
  // No caching happens here
  ```
- ### Summary:
- **Caching** improves performance by reducing network calls.
- Next.js automatically caches data fetched with the `fetch()` function.
- You can control caching by using options like `cache: 'no-store'` and `next: { revalidate: X }`.
- Third-party libraries like **Axios** do not support this automatic caching.

- By understanding and leveraging caching in **Next.js**, you can make your applications more efficient and responsive.
---

# Static and Dynamic Rendering.
- **Static Rendering** - Next.js will pre-render pages or components during the build process, so the content is generated **once** at **build time**. When users request these pages, the pre-rendered content is fetched directly from **Next.js's cache** (stored on the **file system**). This approach speeds up page delivery since the content does not need to be re-rendered on each request.

- ### Comparison with Dynamic Rendering
  - **Static Rendering**: Happens **at build time**, ideal for pages with static content. It leverages caching to serve the same content repeatedly without needing to re-render.
  - **Dynamic Rendering**: Happens **at request time**, meaning that the page is re-rendered every time it is requested. This is used for pages that have frequently changing or dynamic data.
- ### Example: Adding a Timestamp
- To see static rendering in action, consider a page that displays a **list of users** along with a **timestamp**. You can render the current time using the `Date` object.
  ``` tsx 
  //app/users/pages.tsx
  //...
  const UsersPage = async () => {
    const res = await fetch("https://jsonplaceholder.typicode.com/users");
    const users: User[] = await res.json();

    return (
      <>
        <h1>Users</h1>
        {/* add this time stamp to see when the page is rendering */}
        <p>{new Date().toLocaleTimeString()}</p>
  // ...
  ```
  [Source code](https://github.com/Rumindu/next-app/blob/3bc0ad1de1610920fe8560d6a628a6c1af681be3/app/users/page.tsx)
- In **development mode**(`npm run dev`), refreshing the page will update the timestamp because the page is dynamically re-rendered with each request.
- However, in **production mode**, after building the application with `npm run build`,then `npm start`, the timestamp **will not change** upon refreshing. This is because **Next.js** treats the page as **static**, caching it and serving the same pre-rendered content.
- ### Default Caching Behavior in Next.js
- By default, **Next.js** caches data when using the `fetch()` function, treating it as **static data**. When rendering a page that fetches data:
  - **Next.js** recognizes that the data is static, so it renders the page at build time.
  - This **static rendering** allows for fast retrieval of content since the data is already available in the cache.
- ### Disabling Caching for dynamic rendering
- If the data on your page changes frequently, you can **disable caching** by passing an options object to the `fetch()` function. Here's how to do it:
  ```tsx 
  const res = await fetch(
    'https://jsonplaceholder.typicode.com/users', 
    {cache: 'no-store'}
  );
  ```
  [Source code](https://github.com/Rumindu/next-app/blob/99fc602c2de97eae13bd722714747af5aa55d636/app/users/page.tsx)
  - By setting `cache: 'no-store'`, you tell **Next.js** that the data is dynamic and should not be cached. This will force **Next.js** to fetch new data every time the page is requested, resulting in **dynamic rendering**.

- ### Building the Application for Production

- To see static rendering in production, follow these steps:
  1. Run `npm run build` to build the application for production. During the build process, **Next.js** will generate routes and pre-render any static pages.
  2. After the build completes, run `npm start` to start the application in production mode.
  3. When you visit the page in the browser, you will notice that the **timestamp** is not changing upon refreshing. This is because the page was **statically rendered** at build time.

- If you inspect the routes in the terminal after building the application, you’ll see **icons** next to each route:
  - **Circle icons** represent static pages (statically rendered).
  - **Lambda icons** represent pages that are rendered dynamically on the server at request time (server-side rendering).
- #### Recap of Rendering in Next.js
- **Rendering on the Client**: Happens after the page is loaded in the browser. Ideal for interactive, dynamic content.
- **Static Rendering (Build Time)**: Happens during the build process. Pages with static content are generated once and cached.
- **Dynamic Rendering (Request Time)**: Happens on the server for every user request. Suitable for pages with frequently changing data.
- With static rendering, you can significantly improve your app’s performance by caching content that doesn't change often, and Next.js provides the flexibility to handle both static and dynamic rendering based on your data needs.