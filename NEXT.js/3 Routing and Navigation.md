
 In this section, we'll dive deeper into routing and navigation. You will learn 
 - how to define Dynamic routes 
 - access route and query stream parameters, 
 - create layouts 
 - show, loading user interfaces
 - handle errors.
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
      const UserDetailPage = ({ params: { id } }: Props) => {
        return <div>UserDetailPage {id}</div>;
      };
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

- ## 1. **Defining Query String Parameters:**

- A query string is the part of a URL that comes after a `?` and allows for dynamic data to be passed. For example, a URL like `/products?sortOrder=price` has a query string parameter `sortOrder` with the value `price`.

- ## 2. **Accessing Query String Parameters:**

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
  ![](assets/Pasted%20image%2020240925201248.png)

- ## Implementing Sorting in a Users Table Using Query Parameters steps:
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
  - On the **users page**, destructure the `searchParams` to extract the `sortOrder` parameter.
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

- **3. Passing the `sortOrder` to Components**:
  - Once you've accessed the query string parameter (`sortOrder`), pass it down as a **prop** to the `UserTable` component.
    ``` tsx 
    // app/users.page.tsx
    <UserTable sortOrder={sortOrder} />
    ```
    
- **4. Implementing Sorting Logic in the `UserTable`**:
  - In the `UserTable` component, define an interface for props that includes `sortOrder`.
  - Use a sorting library like `fast-sort` to sort the users array based on the `sortOrder` value (either by **name** or **email**).
    ``` tsx 
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

