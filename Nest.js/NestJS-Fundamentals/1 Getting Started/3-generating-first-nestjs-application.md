# 3. Generating our first NestJS Application

<!-- omit from toc -->

## Table of Contents

- [Creating a New NestJS Project](#creating-a-new-nestjs-project)
- [Project Setup Process](#project-setup-process)
- [Package Manager Selection](#package-manager-selection)
- [Installation and Scaffolding](#installation-and-scaffolding)
- [Navigating to Project Directory](#navigating-to-project-directory)
- [Starting the Application](#starting-the-application)
- [Testing the Application](#testing-the-application)
- [Key Points](#key-points)
- [Links/References](#linksreferences)

## Creating a New NestJS Project

- **CLI Command**: Use the Nest CLI to generate a new application

```bash
nest new
```
![NestJS New Project Command](assets/Pasted%20image%2020250903114430.png)

- **Project naming**: CLI prompts for project name

## Project Setup Process

- **CLI automation**: Handles all heavy lifting automatically
  - File structuring
  - Installation process
  - Configuration setup
  - Dependency management
![NestJS Project Name Prompt](assets/Pasted%20image%2020250903114523.png)
- **No manual work**: Everything is automated without user intervention

## Package Manager Selection

- **CLI prompt**: Choose preferred package manager
- **Options available**:
  - NPM (recommended for course)
  - Yarn (alternative option)
![NestJS Package Manager Selection](assets/Pasted%20image%2020250903114732.png)
- **Flexibility**: Choose based on personal preference

## Installation and Scaffolding

- **Process duration**: Approximately 1 minute
- **Automated tasks**:
  - Application scaffolding
  - Dependency installation
  - Project structure creation
  - Configuration files setup
![NestJS Installation Process](assets/Pasted%20image%2020250903114958.png)

- **Complete setup**: Everything ready to start development immediately

## Navigating to Project Directory

- **Directory change**: Move into the newly created project

```bash
cd iluvcoffee
```

- **Ready-to-use**: Application has everything needed to start with NestJS
- **Complete structure**: All necessary files and folders created

## Starting the Application

- **Start command**: Launch the development server

```bash
npm run start
```
![NPM Run Start Command](assets/Pasted%20image%2020250903115154.png)

- **Server details**:
  - HTTP server starts automatically
  - Default port: 3000
  - Development mode enabled

## Testing the Application

- **Browser navigation**: Open application in web browser
- **URL**: `http://localhost:3000`
- **Expected output**: "Hello World!" message
![Hello World Output](assets/Pasted%20image%2020250903115219.png)

- **Success confirmation**: Application running from your own NestJS server

## Key Points

- **CLI automation**: `nest new` command handles complete project setup
- **Project naming**: Use descriptive names (course example: "iluvcoffee")
- **Package manager choice**: NPM or Yarn support available
- **Zero configuration**: CLI creates ready-to-use application structure
- **Quick start**: From creation to running application in minutes
- **Default port**: Application runs on localhost:3000
- **Immediate feedback**: "Hello World!" confirms successful setup
- **Complete development environment**: All dependencies and configuration included
- **Effortless setup**: No manual file creation or dependency management required

## Links/References

- **Video**: 3. Generating our first NestJS Application (Duration: 03:54)
- **Course**: NestJS Fundamentals - Official Tutorial
- **Previous Lesson**: [2. Installing the NestJS CLI](2-installing-nestjs-cli.md)
- **Next Topic**: Exploring the generated NestJS project structure
- **Local Application**: http://localhost:3000

---

**Created**: September 2, 2025  
**Last Modified**: September 2, 2025
