# 4. Use Route Parameters

<!-- omit from toc -->

## Table of Contents

- [Overview](#overview)
- [Understanding Route Parameters](#understanding-route-parameters)
- [Creating Dynamic Routes](#creating-dynamic-routes)
- [Using the @Param() Decorator](#using-the-param-decorator)
- [Accessing Specific Parameters](#accessing-specific-parameters)
- [Testing Route Parameters](#testing-route-parameters)
- [Key Points](#key-points)
- [Links/References](#linksreferences)

## Overview

- Static routes don't work when you need to accept dynamic data
- Route parameters allow capturing dynamic values from URLs
- Essential for REST APIs that work with specific resource IDs
- NestJS provides decorators to easily extract route parameters

## Understanding Route Parameters

- Static routes: `/coffees` - always the same path
- Dynamic routes: `/coffees/123` - where `123` is a variable ID
- Route parameter tokens capture dynamic values at specific URL positions
- Parameters are passed into controller methods automatically

## Creating Dynamic Routes

- Use colon syntax (`:parameter`) to define route parameters in the `@Get()` decorator
- Parameter tokens capture values from the URL path

```typescript
// coffees.controller.ts
import { Controller, Get, Param } from "@nestjs/common";

@Controller("coffees")
export class CoffeesController {
  @Get(":id") // Dynamic route parameter
  findOne(): string {
    return "This action returns a specific coffee";
  }
}
```

- The `:id` token creates a dynamic segment in the route
- Route becomes `/coffees/:id` where `:id` can be any value

## Using the @Param() Decorator

- Extract route parameters using the `@Param()` decorator
- Import from `@nestjs/common` package
- Can access all parameters or specific ones

```typescript
@Controller("coffees")
export class CoffeesController {
  @Get(":id")
  findOne(@Param() params): string {
    return `This action returns coffee #${params.id}`;
  }
}
```

- `@Param()` without arguments returns all route parameters as an object
- Access individual parameters using dot notation: `params.id`

## Accessing Specific Parameters

- Pass parameter name to `@Param()` to get specific parameter directly
- More convenient when you only need one parameter

```typescript
@Controller("coffees")
export class CoffeesController {
  @Get(":id")
  findOne(@Param("id") id: string): string {
    return `This action returns coffee #${id}`;
  }
}
```
[source code](https://github.com/Rumindu/Learn-NestJS-Fundamentals/blob/2bf091e16bb1ca19c2b00274a9cfaa62f49a9694/src/coffees/coffees.controller.ts)
- `@Param('id')` directly extracts the `id` parameter
- Parameter is typed as `string` for better type safety
- Cleaner and more explicit than accessing the full params object

## Testing Route Parameters

- Use Insomnia to test dynamic routes
- Make GET request to `http://localhost:3000/coffees/123342hagfdsw`
- Verify that the ID is captured correctly
  ![testing route parameter 123342hagfdsw](assets/Pasted%20image%2020250907163307.png)

- Change the ID to test different values: `/coffees/10`
- Route should dynamically capture any value passed
![testing route parameter 10](assets/Pasted%20image%2020250907163410.png)

- Parameters work with any string or number value
- Route becomes completely dynamic and reusable

## Key Points

- Route parameters capture dynamic values from URL paths
- Use colon syntax (`:parameter`) in route decorators to define parameters
- `@Param()` decorator extracts route parameters in controller methods
- `@Param()` without arguments returns all parameters as an object
- `@Param('name')` extracts a specific parameter directly
- Parameters are always received as strings by default
- Essential for REST APIs that work with resource identifiers
- Routes become dynamic and can handle any ID or value
- Type parameters as `string` for better TypeScript support
- Test dynamic routes thoroughly with different parameter values

## Links/References

- [route-parameters](https://docs.nestjs.com/controllers#route-parameters)
- **Video:** 4. Use Route Parameters (Duration: 02:05)
- **Previous:** [3. Creating a Basic Controller](3-creating-a-basic-controller.md)
- **Next:** [Coming Next...]

---

**Created:** September 7, 2025  
**Last Modified:** September 7, 2025
