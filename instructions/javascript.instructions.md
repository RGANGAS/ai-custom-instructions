# Instructions for writing JavaScript

## Project Overview

- JavaScript only scope - do not introduce TypeScript-specific syntax, declarations, or .d.ts files

## Code Style/Quality

### Naming Conventions

- Use camelCase for variables and functions; PascalCase for constructors and classes
- Use descriptive names that clearly indicate purpose
- Use UPPER_SNAKE_CASE for constants that are module-level or global
- Prefix event handler functions with "handle" (e.g., handleClick).

### Code Structure

- Emit code already in idiomatic JavaScript (ES modules or CommonJS, consistent with project context)
- Use accurate imports/requires with no unused symbols
- Use explicit exports; avoid default exports when multiple named exports improve clarity
- Make minimal code changes and only modify relevant sections
- Order functions so that those composing others appear earlier in the file

## Linting/Formatting

- Emit code already formatted according to project standards
- Ensure consistent indentation, spacing, and semicolon usage
- Follow established ESLint, Prettier, or Biome configurations when present in the project

## Design Patterns

### Data Structures and State Management

- Use functional purity where feasible; isolate side effects (I/O, logging) at edges
- Use immutable data patterns when appropriate; avoid direct mutation of shared state
- Structure data with clear, predictable shapes; use consistent property naming

### Validation

- Implement input validation at function boundaries
- Validate and sanitize all user inputs
- Validate data types and required properties before processing
- Use parameterized queries for database operations
- Escape output appropriately for the target context (HTML, SQL, etc.)

### Module Organization

- Keep modules focused on single responsibilities
- Use clear separation between pure functions and side-effect operations
- Organize related functionality into cohesive modules

## Error Handling

- Use consistent error handling patterns throughout the codebase
- Provide meaningful error messages that help with debugging
- Use appropriate error types for different failure scenarios
- Handle async errors properly with try/catch or .catch() methods
- If you encounter a bug or suboptimal code, add a TODO comment outlining the problem

## Logging

- Ensure logs are structured and never leak sensitive data
- Use consistent log level semantics across the application
- Include relevant context in log messages for debugging
- Implement appropriate log levels (error, warn, info, debug)

## Test Writing

- Write isolated, deterministic tests; avoid reliance on real external services (mock/stub carefully)
- Keep test utilities small and reusable; share common helpers when broadly useful
- Structure tests with clear arrange/act/assert patterns
- Test both success and failure scenarios
- Ensure tests are independent and can run in any order

## Documentation Standards

### JSDoc Guidelines

- Provide JSDoc comments for public-facing functions where they add clarity
- Document parameters, return values, and expected behavior
- Include examples for complex functions or APIs

### Code Comments

- Write self-documenting code; use inline comments sparingly and focus on non-obvious functionality
- Explain "why" rather than "what" when comments are necessary

## Security

- Never put literal secrets anywhere in code
- Use environment variables or secure configuration management for sensitive data
- Implement proper authentication and authorization checks
