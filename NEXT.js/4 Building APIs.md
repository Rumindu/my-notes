# Creating an API Endpoint to Getting a Collection of Objects in Next.js

In Next.js, you can create API endpoints to handle HTTP requests like retrieving, creating, or updating data. Here’s how to create an endpoint that returns a collection of objects.

1. **API Folder Structure**

   - Under the `app` folder, create an `api` folder (this is not required but is a common convention).
   - Inside the `api` folder, you can create additional folders for specific endpoints (e.g., `users`).

2. **Using a Route File**

   - Instead of adding a `page.tsx` file to the `users` folder (which is used for returning HTML content), you create a **route file** (`route.tsx`) to handle HTTP requests.
   - You can either have a **page** file or a **route** file in a folder, but not both.

3. **Route Handler**

   - A **route handler** is a function that handles an HTTP request and returns a response. For GET requests, define an exported `GET` function.
   - Here’s a sample code to create a `GET` request handler that returns JSON data:
      ``` ts
      import {NextResponse} from "next/server";

      export function GET() {
        return NextResponse.json([
          { id: 1, name: 'Mosh' },
          { id: 2, name: 'John' },
        ]);
      }
      ```

4. **Returning JSON Data**

   - The `GET` function uses `NextResponse.json()` from the `next/server` package to return JSON data (e.g., a list of users).

5. **Avoiding Caching**

   - If the request object (of type `NextRequest` from `next/server`) is not used in this function, Next.js may cache the result by default. To prevent caching and always get fresh data, keep the request parameter in the function signature:
      ``` ts 
      import { NextRequest, NextResponse } from "next/server";

      export function GET(request: NextRequest) {
        return NextResponse.json([
          { id: 1, name: 'Mosh' },
          { id: 2, name: 'John' },
        ]);
      }
      ```
      [source code](https://github.com/Rumindu/next-app/blob/41aba0ab924c1e492b24395db89677279ab37068/app/api/users/route.tsx)

6. **Accessing the Endpoint**

   - Once this is set up, you can access the API at `localhost:3000/api/users` from postman or browser, and it will return a collection of user objects in JSON format.
---

# Creating an API Endpoint for Getting a Single Object in Next.js

To create an API endpoint for retrieving a single object, we can utilize dynamic route parameters in Next.js.

1. **Dynamic Route for ID Parameter**

   - In the `users` folder (inside the `api` folder), create a new folder named `[id]` where `[id]` is wrapped in square brackets. This signifies a dynamic route parameter for the user ID.
   - Inside this `[id]` folder, create a `route.tsx` file to handle the HTTP request.

2. **Defining the Route Handler for a GET Request**

   - The `GET` request is used to retrieve a specific user by their ID.
   - First, import `NextRequest` and `NextResponse` from the `next/server` package.
   - The function to handle the GET request looks like this:
      ``` tsx
      // api/users/[id]/route.tsx 
      import { NextRequest, NextResponse } from "next/server";

      export function GET(
        request: NextRequest,
        { params }: { params: { id: number } }
      ) {
        // Simulate checking for a valid user
        if (params.id > 10)
          return NextResponse.json({ error: "User not found" }, { status: 404 });

        // If user is found, return a mock user object
        return NextResponse.json({ id: 1, name: "Mosh" });
      }
      ```
      [source code](https://github.com/Rumindu/next-app/blob/a5efa8010da9d91598545581f4936b02dff815a2/app/api/users/%5Bid%5D/route.tsx)

3. **Handling Route Parameters**

  - The `params` object, containing the `id`, is destructured directly in the function’s second parameter.
  - In a real application, this `id` would be used to fetch the user data from a database.

4. **Returning the Response**

   - If the `id` is greater than 10 (used as an example rule), it returns a 404 error using `NextResponse.json()` with a status of 404.
   - Otherwise, it returns a mock user object. In this case, a hardcoded user with the ID and name is returned.

5. **Testing the API Endpoint**

   - Visiting `/api/users/1` will return the mock user object:
       
      ```json
      {
        "id": 1,
        "name": "Mosh"
      }
      ```
   - Visiting `/api/users/11` (since the ID is greater than 10) will return a 404 error with the message:
       
      ``` json
      {
        "error": "User not found"
      }
      ```
      
This approach is useful when you need to fetch a specific resource (like a user) based on a dynamic URL parameter in your Next.js application.

---

# Creating an API Endpoint for Posting Data in Next.js

To create an API endpoint for submitting data (e.g., creating a new user) via a POST request in Next.js, follow these steps:

1. **POST Endpoint Setup**

   - In the `users` folder (inside the `api` folder), open the `route.tsx` file.
   - Export a function called `POST`, which handles POST requests.
   - Import `NextRequest` and `NextResponse` from `next/server`.

2. **Reading Request Body**

   - The request body is read using ==`request.json()`, which returns a promise. So, the function must be `async`==.
   - Example of reading the request body:
      ``` tsx 
      export async function POST(request: NextRequest) {
        const body = await request.json();
        return NextResponse.json(body);
      }
      ```    
   - This function currently just echoes the sent data in the response.

3. **Testing with Postman**

   - Since browsers can’t directly send POST requests with a body, tools like **Postman** are used.
   - To test:
      1. Change the request type to **POST** in Postman.
      2. Set the URL to `http://localhost:3000/api/users`.
      3. In the **Body** tab, select **raw** and **JSON**.
      4. Create a JSON object, such as `{"name": "Mosh"}`, and send the request.
      5. You should receive a response with the same data you sent.

4. **Generating IDs**

   - To simulate an ID being generated (normally done by a database), you can hardcode an ID for now:
      ``` tsx 
      return NextResponse.json({ id: 1, name: body.name });
      ```

5. **Validation**

   - Basic validation is crucial. For instance, if the `name` property is missing or empty, return a 400 error (bad request):
      ``` tsx 
      if (!body.name) {
        return NextResponse.json({ error: "Name is required" }, { status: 400 });
      }
      ```


6. **Final Code**
   - If the validation passes, return the newly created object with status 201 (created). 200 is okay. But as convention pass 201 status code in the response

   - The final implementation for the POST endpoint:
      ``` tsx 
      export async function POST(request: NextRequest) {
        const body = await request.json();
        if (!body.name) 
          return NextResponse.json({ error: 'Name is required'}, { status: 400 })
        //201 is the status code for created
        return NextResponse.json({ id: 1, name: body.name }, { status: 201 });
      }
      ```
      [source code](https://github.com/Rumindu/next-app/blob/206e2d06a1e85698cfb2b1e62a4467d85cd23731/app/api/users/route.tsx)

7. **Testing Validation in Postman**

   - Test by removing the `name` field or leaving it empty. The response should be a 400 status with an error message like "Name is required".
   - When the `name` is provided, the response should include the user object, and the status should be 201, indicating successful creation.
---

# Updating an API Object in Next.js

To update an object like a user via an API endpoint in Next.js, follow these steps:

1. **PUT Request Setup**

   - To update a user, you should send a PUT request to the endpoint representing an individual user (e.g. `/api/users/1`). This request should include a user object in the body.
   - Inside the `users/[id]` folder, open the `route.tsx` file.
   - Export a function called `PUT` to handle PUT requests for updating objects, just like how the GET request was handled.
   - Use the `NextRequest` and `NextResponse` from `next/server`.

2. ==**Choosing Between PUT and PATCH**==

   - **PUT** is used to replace an entire object, while **PATCH** is for updating specific properties. In this case, Mosh recommends using `PUT` to replace the user.

3. **Accessing Route Parameters**

   - Just like in the GET request, access the route parameter (ID) using the following approach:
      ``` tsx 
      export async function PUT(
        request: NextRequest,
        { params }: { params: { id: number } }
      ) {//...
      }
      ```

4. Full code

    ``` tsx 
    export async function PUT(
      request: NextRequest,
      { params }: { params: { id: number } }
    ) {
      //request.json() returns a promise, so the function must be marked async
      const body = await request.json();

      // Validation: Name is required
      if (!body.name)
        return NextResponse.json({ error: "Name is required" }, { status: 400 });

      // Simulate user not found for IDs greater than 10
      if (params.id > 10)
        return NextResponse.json({ error: "User not found" }, { status: 404 });

      // Simulate user update
      return NextResponse.json({ id: 1, name: body.name });
    }
    ```
    

5. **Testing with Postman**

   - To test the PUT request, use Postman:
     1. Set the request type to **PUT**.
     2. Use the URL `http://localhost:3000/api/users/1`.
     3. In the **Body** tab, select **raw** and **JSON**.
     4. Provide a valid JSON object, e.g., `{"name": "Mosh Updated"}`.
     5.  Send the request to see the updated user data in the response.

6. **Handling Errors**

   - If the `name` field is missing or empty, return a `400 Bad Request` response with the message "Name is required."
   - If the user doesn't exist (e.g., `id > 10`), return a `404 Not Found` response with the message "User not found."
   - For successful updates, return a `200 OK` status (or `201 Created` if a new object is created), along with the updated user object.
---

# Deleting an Object in Next.js API Route (DELETE Method)


To delete a user, send a `DELETE` request to the endpoint that represents the specific user (e.g., `/api/users/1`). This endpoint should handle the request, validate the user ID, and simulate the deletion of the user from the database.

1. **File Structure**

   - Inside the `users/[id]` folder, open the `route.ts` file.
   - Export a new handler function for handling the `DELETE` request.

2. **Destructuring Route Parameters**

   - Similar to the `PUT` handler, you need to access the route parameters and the request object. Here’s how to destructure the parameters directly in the function signature:
   ``` tsx 
     export async function DELETE(
       request: NextRequest,
       { params }: { params: { id: number } }
     ) {// Use params.id to identify the user to delete
     }
   ```

3. **Handling the Request**

   1. **Simulate Fetching User from Database**:
       
       - In a real application, you would fetch the user from the database.
       - For simulation purposes, assume that if the `id` is greater than `10`, the user does not exist. Return a `404 Not Found` response if the user is not found.
   
   2. **Simulate Deleting User**:
       
       - If the `id` is valid (e.g., `id <= 10`), simulate deleting the user by returning a `200 OK` response.
       - You can either return an empty response or include details of the deleted user in the response body. This decision depends on your application's requirements.

4. **Full Code Example**:

    ``` tsx 
    //app/api/users/[id]/route.tsx
    export function DELETE(
      request: NextRequest,
      { params }: { params: { id: number } }
    ) {
      // Simulate user not found for IDs greater than 10
      if (params.id > 10)
        return NextResponse.json({ error: "User not found" }, { status: 404 });
    // Simulate user deletion
      return NextResponse.json({});
    }
    ```
    [source code](https://github.com/Rumindu/next-app/blob/fbd69abc3ebfb95b6eb0fc128749e742728cfdb4/app/api/users/%5Bid%5D/route.tsx)

5. **Testing with Postman**

- Use a tool like Postman to test the `DELETE` request.
    - Set the request type to `DELETE`.
    - The endpoint should be `/api/users/1` (or any valid user ID).

- If the user doesn't exist (e.g., `id > 10`), the response will be:

  - **404 Not Found** with the message "User not found."

- For valid users (e.g., `id <= 10`), the response will be:

  - **200 OK** with an empty response body.
---

# Validating Requests with Zod in Next.js

This note covers how to validate request bodies using the Zod library in a Next.js API route, which simplifies the process of validating complex objects.

1. **Why Use a Validation Library Like Zod?**

   - In a typical `PUT` or `POST` request, you might use `if` statements to validate incoming request data (e.g., checking for the presence of a `name` field). However, as objects become more complex, these `if` statements can become unwieldy. A validation library like [Zod](https://zod.dev/) helps by providing a more structured and reusable approach to validation.

2. **Installing Zod**

   - First, install Zod using npm:
      ``` bash
      npm install zod
      ```

3. **Creating a Schema for User Validation**

   - In the `/api/users` folder, create a new file called `schema.ts`.
   - Define the schema for the user object using Zod:

      ``` ts 
      import { z } from 'zod';

      const schema = z.object({
        //from adding second parameter to min() overriding the default error message ""String must contain at least 3 character(s)"
        name: z.string().min(3,"Name must be at least 3 characters long"),
        // You can add other properties like email or age, e.g.
        // email: z.string().email(),
        // age: z.number().min(18),
      });

      export default schema;
      ```
      [source code](https://github.com/Rumindu/next-app/blob/7623d3dd8b3ec22d08e7fec45910a5e0cc1c7038/app/api/users/schema.ts)


   - The schema specifies that the `name` field is a string and must be at least 3 characters long. You can easily extend this to validate additional fields (e.g., `email`, `age`).

4. **Using the Schema in the Route Handler**

   - Go back to your API route file (e.g., `/api/users/[id]/route.ts` for `PUT` requests).
   - Import the schema:
      ``` tsx 
      // app/api/users/[id]/route.tsx
      import schema from "../schema";
      ```
   - Replace the manual validation (`if` statements) with Zod validation:

      ``` tsx 
      // app/api/users/[id]/route.tsx
      export async function PUT(
        request: NextRequest,
        { params }: { params: { id: number } }
      ) {
        //request.json() returns a promise, so the function must be marked async
        const body = await request.json();

        // Validate request body using zod
        const validation = schema.safeParse(body);

        // Check if validation failed
        if (!validation.success)
          return NextResponse.json(validation.error.errors, { status: 400 });

        // Simulate user not found for IDs greater than 10
        if (params.id > 10)
          return NextResponse.json({ error: "User not found" }, { status: 404 });

        // Simulate user update
        return NextResponse.json({ id: 1, name: body.name });
      }
      ```
      [source code](https://github.com/Rumindu/next-app/blob/7623d3dd8b3ec22d08e7fec45910a5e0cc1c7038/app/api/users/%5Bid%5D/route.tsx)

5. **Safe Parsing vs. Parsing**

   - **`safeParse`**: This method does not throw exceptions. Instead, it returns an object with a `success` property (true or false) and either the validated data or an error.
   - **`parse`**: This method throws an exception if the validation fails.
   - In this example, we use `safeParse` to avoid exceptions and handle errors gracefully.

6. **Handling Validation Errors**

   - If validation fails, return the detailed error messages generated by Zod:
      ``` tsx 
      // app/api/users/[id]/route.tsx
      if (!validation.success)
          return NextResponse.json(validation.error.errors, { status: 400 });
      ```
   - Zod provides a structured error object, which contains details like the specific field that failed validation, error codes, and human-readable messages.

7. **Testing in Postman**

   - Use Postman to test the endpoint. For example, send a `PUT` request to update a user:
     - Endpoint: `/api/users/1`
     - Body:
        ``` json 
        {
          "name":""
        }
        ```
   - The response should be a `400 Bad Request` with an error message such as:
      ``` json 
      [
        {
          "code": "too_small",
          "minimum": 3,
          "type": "string",
          "inclusive": true,
          "exact": false,
          "message": "Name must be at least 3 characters long",
          "path": [
            "name"
          ]
        }
      ]
      ```
---

# Exercise: Building a Products API in Next.js

1. **Goal**

   - Create an API at `/api/products` that returns a list of products (each with an `id`, `name`, and `price`) and allows adding new products through `POST` requests with validation.


2. Getting products with `GET`

   - In the `/api` folder, create a new folder called `products`, then add a `route.tsx` file inside it.
   - First, export the `GET` function, which returns a hardcoded list of products:

      ``` tsx 
      import { NextRequest, NextResponse } from "next/server";
      import schema from "./schema";

      export function GET(request: NextRequest) {
      return NextResponse.json([
         { id: 1, name: "Milk", price: 2.0 },
         { id: 2, name: "John", price: 3.5 },
      ]);
      }
      ```
      [source code](https://github.com/Rumindu/next-app/blob/1af44313b51c27e86c36c1dfdae481ec913df5c9/app/api/products/route.tsx)

   - Test this by sending a `GET` request to `/api/products` via Postman. You should receive a `200` response with the list of products.

3. **Validating Input with Zod**

   - Create a `schema.ts` file inside the `products` folder to define validation rules for a product using Zod:
      ``` ts
      import { z } from "zod";

      const schema = z.object({
      name: z.string().min(3),
      price: z.number().min(1).max(100)
      });

      export default schema;
      ```
      [source code](https://github.com/Rumindu/next-app/blob/1af44313b51c27e86c36c1dfdae481ec913df5c9/app/api/products/schema.ts)

4. **Creating Products with `POST` and Applying Validation**
   - Add a POST function to handle new product creation in the `/api/products/route.tsx`
   - Import the schema and use `safeParse` to validate the incoming request:
      ``` tsx 
      import productSchema from './schema';

      export async function POST(request: NextRequest) {
      const body = await request.json();
      // Validate using Zod
      const validation = schema.safeParse(body);

      if (!validation.success)
         return NextResponse.json(validation.error.errors, { status: 400 });

      // If validation passes, create a new product
      return NextResponse.json(
         { id: 10, name: body.name, price: body.price },
         { status: 201 }
      );
      }
      ```
        [source code](https://github.com/Rumindu/next-app/blob/1af44313b51c27e86c36c1dfdae481ec913df5c9/app/api/products/route.tsx)

5. **Testing in Postman**

   - **`GET` request**: Send a `GET` request to `/api/products` to receive the list of products.
       
   - **`POST` request**:
       
       - Set up a `POST` request to `/api/products`.
       - Test validation by sending invalid data, such as an empty object `{}`. You should receive a `400 Bad Request` response with errors for the missing `name` and `price`.
       - Sending valid data (e.g., `{"name": "Eggs", "price": 5}`) should return a `201 Created` response with the new product.



6. **Key Points**

   - **Hardcoded Data**: For simplicity, hardcoded product data is used. In real-world apps, this data would come from a database.
   - **Validation**: Zod helps validate the request body, ensuring that only valid product data is processed.
   - **Explicit Property Setting**: Instead of using the spread operator (`...body`), set the properties explicitly to avoid malicious users sending unwanted data. Use this 
     
      ``` tsx
      return NextResponse.json(
         { id: 10, name: body.name, price: body.price },
         { status: 201 }
      ); 
      ``` 

      instead of

      ``` tsx 
      return NextResponse.json(
         { id: 10, ... body},
         { status: 201 }
      );
      ```` 