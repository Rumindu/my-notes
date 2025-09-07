# 3. Creating a Basic Controller

<!-- omit from toc -->

## Table of Contents

- [Overview](#overview)
- [What are Controllers](#what-are-controllers)
- [Generating a Controller with Nest CLI](#generating-a-controller-with-nest-cli)
- [Adding HTTP Route Handlers](#adding-http-route-handlers)
- [Testing the Controller](#testing-the-controller)
- [Nested Routes](#nested-routes)
- [CLI Tips and Best Practices](#cli-tips-and-best-practices)
- [Key Points](#key-points)
- [Links/References](#linksreferences)

## Overview

- Controllers are fundamental building blocks of NestJS applications
- Handle incoming requests and return responses to clients
- Use decorators and classes to define routing and behavior
- Generated automatically using the Nest CLI with proper structure

## What are Controllers

- Classes decorated with `@Controller()` that handle HTTP requests
- Responsible for receiving requests and returning responses
- Use decorators to define routes and HTTP methods
- Building blocks that organize application logic by feature

## Generating a Controller with Nest CLI

- Use the Nest CLI to generate controllers automatically
- Full command: `nest generate controller`
- Shorthand: `nest g co`
- CLI prompts for controller name

```bash
# Generate a controller
nest generate controller
# Or shorthand
nest g co
```
![Terminal showing controller generation](assets/Pasted%20image%2020250906174534.png)

- Example: Creating a "coffees" controller for a coffee shop app
- CLI automatically creates:
  - Controller file (`coffees.controller.ts`)
  - Test file (`coffees.controller.spec.ts`)
  - Updates AppModule with new controller
![Generated controller files in VS Code](assets/Pasted%20image%2020250906174659.png)
![Updates AppModule](assets/Screenshot%202025-09-06%20174832.png)

## Adding HTTP Route Handlers

- Controllers use the `@Controller()` decorator with a route prefix
- Individual methods use HTTP verb decorators (`@Get()`, `@Post()`, etc.)

```typescript
// coffees.controller.ts
import { Controller, Get } from '@nestjs/common';

@Controller('coffees') // Route prefix
export class CoffeesController {
  @Get() // GET /coffees
  findAll(): string {
    return 'This action returns all coffees';
  }
}
```
- The `@Controller('coffees')` decorator maps to `/coffees` URL
- Route handlers are methods decorated with HTTP verbs
- Method names can be anything descriptive (e.g., `findAll()`)

## Testing the Controller

- Use Insomnia to test the controller endpoints
- Make GET request to `http://localhost:3000/coffees`
- Initially returns 404 error (generated controller)
``` ts 
import { Controller } from '@nestjs/common';

@Controller('coffees')
export class CoffeesController {}
```
![postman showing 404 error](assets/Pasted%20image%2020250907104428.png)
- After adding the `@Get()` handler, request succeeds
- Returns the string: "This action returns all coffees"
![postman showing successful response](assets/Pasted%20image%2020250907104600.png)

## Nested Routes

- HTTP decorators accept a string parameter for nested paths
- Appends to the controller's base route

```typescript
@Controller('coffees')
export class CoffeesController {
  @Get('flavors') // GET /coffees/flavors
  findAllFlavors(): string {
    return 'This action returns all coffee flavors';
  }
}
```

- Route becomes `/coffees/flavors` instead of just `/coffees`
- Test the nested route in Insomnia
![postman testing nested route](assets/Pasted%20image%2020250907104807.png)

## CLI Tips and Best Practices

- **Generating in specific directories:**

```bash
nest g co modules/abc
# Creates controller in /src/modules/abc/
```

- **Skip test file generation:**

```bash
nest g co coffees --no-spec
```

- **Dry run to preview:**

```bash
nest g co coffees --dry-run
# Shows what will be created without actually creating files
```
![Terminal showing dry run output](assets/Pasted%20image%2020250906180505.png)
- Use dry run to verify file placement before generation
- Helpful for complex directory structures

## Key Points

- Controllers handle HTTP requests and define application routes
- Generated using `nest g co [name]` command
- Use `@Controller()` decorator with route prefix
- HTTP verb decorators (`@Get()`, `@Post()`, etc.) define route handlers
- Automatically registered in AppModule by CLI
- Support nested routes through decorator parameters
- Method names don't affect routing (decorators determine routes)
- CLI provides helpful flags (`--no-spec`, `--dry-run`)
- Building blocks for organizing application logic by feature
- Easy to read and maintain uniform structure

## Links/References

- **Video:** 3. Creating a Basic Controller (Duration: 04:52)
- **Previous:** [2. Running NestJS in Development Mode](2-running-nestjs-in-development-mode.md)
- **Next:** [Coming Next...]

---

**Created:** September 6, 2025  
**Last Modified:** September 6, 2025
