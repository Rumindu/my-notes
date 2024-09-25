[Learn Next.js](https://nextjs.org/learn/dashboard-app)

- # What is streaming?
- Streaming is a data transfer technique that allows you to break down a route(here route means page) into smaller "chunks" and progressively stream them from the server to the client as they become ready.
- There are two ways you implement streaming in Next.js:
  1. At the page level, with the `loading.tsx` file.
  2. For specific components, with `<Suspense>`.
- #### 1. Streaming a whole page with `loading.tsx`
  ``` tsx
  // app/dashboard/loading.tsx
  export default function Loading() {  return <div>Loading...</div>;}
  ```
- `loading.tsx` is a special Next.js file built on top of Suspense, it allows you to create fallback UI to show as a replacement while page content loads.
- Since `<SideNav>` is static, it's shown immediately. The user can interact with `<SideNav>` while the dynamic content is loading.
- The user doesn't have to wait for the page to finish loading before navigating away (this is called interruptable navigation).
- ##### Adding loading skeletons
  ``` tsx
  // app/dashboard/loading.tsx
  import DashboardSkeleton from '@/app/ui/skeletons'; 
  export default function Loading() {
    return <DashboardSkeleton />;
  }
  ```
- ##### Fixing the loading skeleton bug with route groups
- Right now, your loading skeleton will apply to the invoices and customers pages as well Because `loading.tsx` is a level higher than `/invoices/page.tsx` and `/customers/page.tsx` in the file system, Therefore loading Skelton is also applied to those pages.
- We can change this with [Route Groups](https://nextjs.org/docs/app/building-your-application/routing/route-groups). Create a new folder called `/(overview)` inside the dashboard folder. Then, move your `loading.tsx` and `page.tsx` files inside the folder:
```
dashboard
│   layout.tsx
│
├───(overview)
│       loading.tsx
│       page.tsx
```
- Now, the `loading.tsx` file will only apply to your dashboard overview page.
- Route groups allow you to organize files into logical groups without affecting the URL path structure. When you create a new folder using parentheses `()`, the name won't be included in the URL path. So `/dashboard/(overview)/page.tsx` becomes `/dashboard`.
- Here, you're using a route group to ensure `loading.tsx` only applies to your dashboard overview page. However, you can also use route groups to separate your application into sections (e.g. `(marketing)` routes and `(shop)` routes) or by teams for larger applications.
- #### 2. Streaming a component
- Here Instead of streaming the entire page, you can stream specific components on the page using **React Suspense**.
- [example code](https://github.com/Rumindu/nextjs-dashboard-offical-learning-project/tree/01a03ca3e7886da84a228706b94c2156a7647b1c)
- # Partial Prerendering(PPR)
- ==Partial Prerendering is an experimental feature introduced in Next.js 14==.
- In Next.js, if you call a [dynamic function](https://nextjs.org/docs/app/building-your-application/routing/route-handlers#dynamic-functions) in a route/page (like querying your database), ***the entire route/page becomes dynamic.***
- For most web apps built today, you either choose between static and dynamic rendering for your **entire application**, or for a **specific route**.
- However, most routes are _not_ fully static or dynamic. For example, consider an [ecommerce site](https://partialprerendering.com/). You might want to statically render the majority of the product information page, but you may want to fetch the user's cart and recommended products dynamically, this allows you show personalized content to your users.
- # Adding Search and Pagination
- **Debouncing** is a programming practice that limits the rate at which a function can fire. In our case, program only query the database when the user has stopped typing.
- [Debouncing implementation](https://github.com/Rumindu/nextjs-dashboard-offical-learning-project/blob/7a2bc41d619097fe1680c6bfec9be96c652144dc/app/ui/search.tsx)
- ## Pagination
- [Pagination Implementation](https://github.com/Rumindu/nextjs-dashboard-offical-learning-project/tree/693d7acd1a784b9635e2f996e9bbcdd44754de5c)
- # Mutating Data (CRUD)
- ## [What are Server Actions?](https://nextjs.org/learn/dashboard-app/mutating-data#what-are-server-actions)
- React Server Actions allow you to run asynchronous code directly on the server.
- They eliminate the need to create API endpoints to mutate your data. Instead, you write asynchronous functions that execute on the server and can be invoked from your Client or Server Components.
- ## [Creating an invoice](https://nextjs.org/learn/dashboard-app/mutating-data#creating-an-invoice)
- Here are the steps you'll take to create a new invoice:
  1. Create a new route and form to capture the user's input.
  2. Create a Server Action and invoke it from the form.
  3. Inside your Server Action, extract the data from the `formData` object.
  4. Validate and prepare the data to be inserted into your database.
  5. Insert the data and handle any errors.
  6. Revalidate the cache and redirect the user back to invoices page.
- ### 1.Create a new route and form to capture the user's input
  ![](assets/Pasted%20image%2020240921084453.png)
- ### 4. Validate and prepare the data to be inserted into your database.
- use  [Zod](https://zod.dev/)library for validation. 
- ### 6.Revalidate the cache and redirect the user back to invoices page.
- Next.js has a [Client-side Router Cache](https://nextjs.org/docs/app/building-your-application/caching#router-cache) that stores the route segments in the user's browser for a time.
- Along with [prefetching](https://nextjs.org/docs/app/building-your-application/routing/linking-and-navigating#1-prefetching), this cache ensures that users can quickly navigate between routes while reducing the number of requests made to the server.
- ## [Updating an invoice](https://nextjs.org/learn/dashboard-app/mutating-data#updating-an-invoice)
- These are the steps you'll take to update an invoice:
  1. Create a new dynamic route segment with the invoice `id`.
  2. Read the invoice `id` from the page params.
  3. Fetch the specific invoice from your database.
  4. Pre-populate the form with the invoice data.
  5. Update the invoice data in your database.
- # Authentication
- ## [Setting up NextAuth.js](https://nextjs.org/learn/dashboard-app/adding-authentication#setting-up-nextauthjs)
- `pnpm i next-auth@beta`
- Generate a secret key for your application. This key is used to encrypt [cookies](../cookies.md###Cookie%20Tasks%20in%20Authentication:), ensuring the security of user sessions. You can do this by running the following command in vs code's bash terminal.
  ``` shell 
  openssl rand -base64 32
  ```
- 