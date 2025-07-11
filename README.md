# Svelte 5 Demo Application

## Overview

This is a demonstration project built with Svelte 5, showcasing the new features and capabilities of the latest version of the Svelte framework. The application includes several interactive components that highlight Svelte 5's new reactivity system, including `$state`, `$effect`, and `$inspect` features.

## Project Structure

```
├── src/
│   ├── app.d.ts           # TypeScript declarations
│   ├── app.html           # HTML template with global styles
│   ├── lib/               # Library code
│   └── routes/            # SvelteKit routes
│       ├── +page.svelte   # Main page component
│       └── components/    # Reusable components
│           ├── flightTicketBooker.svelte
│           ├── tempratureConverter.svelte
│           └── timer.svelte
├── static/                # Static assets
├── .gitignore             # Git ignore file
├── .npmrc                 # NPM configuration
├── package.json           # Project dependencies and scripts
├── svelte.config.js       # Svelte configuration
├── tsconfig.json          # TypeScript configuration
└── vite.config.ts         # Vite configuration
```

## Features

The application includes three main components that demonstrate different aspects of Svelte 5's capabilities:

### 1. Timer Component

A simple timer that demonstrates Svelte 5's new reactivity system with `$state` and `$effect`. Features include:

- Adjustable duration using a slider
- Visual progress bar
- Automatic start/reset functionality
- Cleanup of intervals when component is destroyed

### 2. Temperature Converter

A bidirectional temperature converter that showcases Svelte 5's class-based state management with private fields and getters/setters. Features include:

- Convert between Celsius and Fahrenheit
- Real-time updates as values change
- Encapsulated state using private class fields

### 3. Flight Ticket Booker

A form-based component that demonstrates form handling and conditional rendering in Svelte 5. Features include:

- One-way or return ticket selection
- Date selection with validation
- Conditional form fields based on ticket type
- Form submission with validation
- State inspection using `$inspect`

## Technologies Used

- **Svelte 5**: The latest version of the Svelte framework with the new reactivity system
- **SvelteKit 2**: Application framework for building Svelte applications
- **TypeScript**: For type safety and better developer experience
- **Vite**: Fast, modern frontend build tool

## Getting Started

### Prerequisites

- Node.js (latest LTS version recommended)
- npm or yarn

### Installation

```bash
npm install
```

### Development

Run the development server:

```bash
npm run dev
```

This will start the development server at `http://localhost:5173`.

### Building for Production

```bash
npm run build
```

### Preview Production Build

```bash
npm run preview
```

## New Svelte 5 Features Demonstrated

### Reactivity

- `$state`: Declares reactive variables
- `$effect`: Runs side effects when dependencies change
- `$inspect`: Debugging tool for reactive state

### Class-based State Management

- Private fields with `#` prefix
- Getters and setters for controlled state updates
- Binding to class properties

## Project Configuration

- **SvelteKit**: Configured with auto adapter for flexible deployment
- **Vite**: Used as the build tool with SvelteKit plugin
- **TypeScript**: Configured for type checking

## License

This project is for demonstration purposes.

## Acknowledgements

- Svelte team for the amazing framework
- SvelteKit for the application framework
- Vite for the build tooling
