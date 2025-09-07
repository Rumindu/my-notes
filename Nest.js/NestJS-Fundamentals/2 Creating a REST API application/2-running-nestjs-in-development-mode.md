# 2. Running NestJS in Development Mode

<!-- omit from toc -->

## Table of Contents

- [Overview](#overview)
- [Development Mode vs Production Mode](#development-mode-vs-production-mode)
- [Starting Development Mode](#starting-development-mode)
- [Hot Reload in Action](#hot-reload-in-action)
- [Testing Changes with Insomnia](#testing-changes-with-insomnia)
- [Key Points](#key-points)
- [Links/References](#linksreferences)

## Overview

- NestJS provides a development mode for enhanced productivity during development
- Offers real-time compilation and automatic server rebuilds on file changes
- Eliminates the need to manually restart the server after code changes
- Significantly speeds up the development workflow

## Development Mode vs Production Mode

- **Production mode:** `npm run start` - Basic application startup
- **Development mode:** `npm run start:dev` - Watch mode with hot reload
- Development mode provides automatic recompilation on file changes
- Server automatically restarts when changes are detected

## Starting Development Mode

- Open terminal in the root directory of your NestJS project
- Run the development command:

```bash
npm run start:dev
```

![Terminal showing development mode startup](assets/Pasted%20image%2020250906174102.png)

- NestJS begins compiling the application in watch mode
- Console shows "actively waiting for file changes" message
- Application starts on `http://localhost:3000` by default

## Hot Reload in Action

- Make changes to any source file (e.g., `app.service.ts`)
- Example: Change `"Hello World"` to `"Hello Nest"` in the service
- Save the file to trigger automatic recompilation

```typescript
// app.service.ts
getHello(): string {
  return 'Hello Nest'; // Changed from "Hello World"
}
```

- Terminal automatically shows rebuild process
- Server restarts without manual intervention
- Changes are reflected immediately

## Testing Changes with Insomnia

- Open Insomnia REST client
- Create a GET request to `http://localhost:3000`
- Hit send to test the endpoint
- Verify the updated response appears ("Hello Nest")
- Near-instant recompilation provides immediate feedback
- No need to manually restart server or refresh connections

## Key Points

- Development mode (`npm run start:dev`) enables watch mode with hot reload
- Automatic recompilation occurs on every file save
- Server restarts automatically without manual intervention
- Provides near-instant feedback for code changes
- Massive productivity boost during development
- Essential for efficient NestJS development workflow
- Works seamlessly with API testing tools like Insomnia
- Watch mode monitors all source files in the project

## Links/References

- **Video:** 2. Running NestJS in Development Mode (Duration: 01:06)
- **Previous:** [1. Prerequisite Install Insomnia](1-prerequisite-install-insomnia.md)
- **Next:** [Coming Next...]

---

**Created:** September 6, 2025  
**Last Modified:** September 6, 2025
