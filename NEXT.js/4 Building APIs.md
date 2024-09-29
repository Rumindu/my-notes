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
      [source code](https://github.com/Rumindu/next-app/blob/3817cf1ba04b82c3ce1e72d3292d975a70f0879a/app/api/users/route.tsx)

7. **Testing Validation in Postman**

   - Test by removing the `name` field or leaving it empty. The response should be a 400 status with an error message like "Name is required".
   - When the `name` is provided, the response should include the user object, and the status should be 201, indicating successful creation.
---
