# 5. Handling Request Body Payload

<!-- omit from toc -->

## Table of Contents

- [Overview](#overview)
- [Understanding Request Bodies](#understanding-request-bodies)
- [The @Body() Decorator](#the-body-decorator)
- [Creating a POST Endpoint](#creating-a-post-endpoint)
- [Testing with postman](#testing-with-postman)
- [Accessing Specific Body Properties](#accessing-specific-body-properties)
- [Validation Considerations](#validation-considerations)
- [Key Points](#key-points)
- [Links/References](#linksreferences)

## Overview

- POST requests typically include data in the request body (payload)
- NestJS provides the `@Body()` decorator to access request payloads
- Similar to `@Param()`, the `@Body()` decorator can access entire body or specific properties
- Essential for creating REST API endpoints that accept data

## Understanding Request Bodies

- Request bodies contain data sent from clients to the server
- Common in POST, PUT, PATCH requests for creating/updating resources
- Usually formatted as JSON in REST APIs
- Contains the payload data that needs to be processed

## The @Body() Decorator

- Extracts data from the request body
- Import from `@nestjs/common` package
- Works similarly to `@Param()` decorator
- Can access entire body or specific properties

```typescript
import { Controller, Post, Body } from "@nestjs/common";
```

## Creating a POST Endpoint

- Add a new POST method to the CoffeesController
- Use `@Post()` decorator for HTTP POST verb
- Use `@Body()` decorator to access request payload

```typescript
// coffees.controller.ts
import { Controller, Get, Post, Body, Param } from "@nestjs/common";

@Controller("coffees")
export class CoffeesController {
  @Get()
  findAll(): string {
    return "This action returns all coffees";
  }

  @Post()
  create(@Body() body): string {
    return body; // Return the entire request body
  }
}
```
[source code](https://github.com/Rumindu/Learn-NestJS-Fundamentals/blob/eca08b180b5cf6f22e169d6b34fdd173166e563f/src/coffees/coffees.controller.ts)
- The `@Body()` decorator extracts the entire request body
- Method returns the body to verify payload is received correctly

## Testing with postman

- Use postman to test the POST endpoint
- Make POST request to `http://localhost:3000/coffees`
- Set content type to JSON and add request body

```json
{
  "name": "Espresso",
  "brand": "Premium Coffee Co",
  "flavors": ["chocolate", "vanilla"]
}
```

- Send the request and verify the response
- Request body should be returned automatically
  ![showing successful POST response](assets/Pasted%20image%2020250907220126.png)

- The endpoint successfully accesses and returns the request payload

## Accessing Specific Body Properties

- Pass a property name to `@Body()` to access specific fields
- Similar to how `@Param('id')` works for route parameters

```typescript
@Controller("coffees")
export class CoffeesController {
  @Post()
  create(@Body("name") name1: string): string {
    return name1; // Only returns the 'name' property
  }
}
```

- Test with the same JSON payload in postman
- Only the 'name' value will be returned
![postman showing specific property response](assets/Pasted%20image%2020250907220541.png)

## Validation Considerations

- **Important Warning:** Accessing specific properties bypasses validation
- When using `@Body('name')`, other properties won't be validated
- This can lead to potential security and data integrity issues
- **Best Practice:** Use the entire body object for proper validation

```typescript
// Recommended approach
@Post()
create(@Body() body): string {
  return body; // Full body allows complete validation
}

// Use with caution
@Post()
create(@Body('name') name: string): string {
  return name; // Other properties won't be validated
}
```

## Key Points

- `@Body()` decorator extracts data from HTTP request bodies
- Essential for POST, PUT, PATCH endpoints that accept data
- Import from `@nestjs/common` package alongside other decorators
- Can access entire body object or specific properties
- `@Body()` returns the complete request payload
- `@Body('property')` returns only the specified property
- **Validation Warning:** Specific property access bypasses validation
- Always consider validation implications when choosing approach
- Test POST endpoints thoroughly with various JSON payloads
- Request body data is automatically parsed and made available
- Similar pattern to `@Param()` decorator for consistency

## Links/References

- **Video:** 5. Handling Request Body Payload (Duration: 02:05)
- **Previous:** [4. Use Route Parameters](4-use-route-parameters.md)
- **Next:** [Coming Next...]

---

**Created:** September 7, 2025  
**Last Modified:** September 7, 2025
