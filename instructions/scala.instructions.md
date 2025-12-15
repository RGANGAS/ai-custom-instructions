# Instructions for Writing Scala

## Project Overview

- Defer to the official Scala Style Guide (https://docs.scala-lang.org/style/), but practices stated here override conflicts.
- Favor clarity, domain-expressive naming, and modular structure.
- Prefer functional style with small, testable functions.

## Code Style and Quality

### Naming Conventions

- Package root: `com.companyname.[line-of-business].[organization].[component-name]`
- UK alternatives: `com.companyname.uk.[component-name]` or `uk.co.companyname.services.[component-name]`
- Modules: Use domain-oriented module names (e.g., `identity`, `payments`, `analytics`)
- Variables and identifiers:
  - Use concise, meaningful, domain-relevant names
  - Avoid Hungarian notation
  - Avoid unnecessary abbreviations or opaque shorthand

### Type Annotations

- Explicitly annotate public method return types for clarity
- Use type annotations for complex expressions where type inference may be unclear
- Use precise types over general ones when domain meaning is important
- Use union types (Scala 3) or sealed traits for representing constrained value sets

## Linting and Formatting

Use Scalafmt with the recommended configuration (Scala 3 shown; adjust dialect for Scala 2.13 projects):

```scala
version = 3.9.7
runner.dialect = scala3
align.preset = more
maxColumn = 120
align.stripMargin = true
rewrite.rules = [RedundantBraces, RedundantParens]
```

For migration preparation (Scala 2 toward 3):

```scala
version = 3.9.7
runner.dialect = Scala212Source3
rewrite.scala3.convertToNewSyntax = true
rewrite.scala3.newSyntax.control = false
align.preset = more
maxColumn = 120
align.stripMargin = true
rewrite.rules = [RedundantBraces, RedundantParens]
```

### Formatting Standards

- Ensure consistent formatting before committing; reject diffs with missing formatting
- Use meaningful indentation and whitespace to enhance readability

## Design Patterns

### Functional Design

- Use functional style with small, testable functions
- Use pure functions to simplify direct testing and reasoning
- Use immutable data structures by default
- Implement algebraic data types using sealed traits and case classes

### Data Structures

- Use case classes for data modeling with automatic equality and copy methods
- Leverage sealed traits for sum types and pattern matching
- Use `Option` over null for optional values

### Data Validation

- Implement validation using applicative functors or validation libraries
- Use type-safe validation that accumulates errors rather than failing fast
- Create domain-specific validation functions that can be composed
- Use compile-time validation through phantom types when possible

### State Management

- Use immutable state transformations
- Implement state machines using sealed traits and pattern matching
- Use functional state management patterns over mutable state
- Use lenses or similar abstractions for deep data structure updates

## Error Handling

- Use `Try`, `Either[Error, Result]`, or custom error types instead of throwing exceptions
- If effect libraries such as ZIO, Cats Effect, or Kyo are used, prefer those in effectful code.
- Handle exceptions at application boundaries (I/O, external service calls)
- Define domain-specific error hierarchies using sealed traits for exhaustive pattern matching
- Include sufficient context in error types for proper handling, logging, and debugging
- Employ proper error handling that doesn't leak sensitive information

## Test Writing

### Testing Framework Guidance

- Encourage property-based testing using ScalaCheck or similar libraries
- Use concrete behavior verification to reduce fragility; minimize mocking
- Use ScalaTest, MUnit, Zio Test, or similar testing frameworks consistently across the project
- Structure tests to mirror domain module organization

### Test Structure Best Practices

- Keep test names behavior-focused and descriptive
- Organize tests by feature or domain concept rather than by class structure
- Use Given-When-Then or Arrange-Act-Assert patterns for clarity
- Write property-based tests for functions with clear mathematical properties
- Use testing behavior over implementation details
- Use direct tests over mocks; properly functionall/y abstracted code should not require mocking

## Documentation Standards

### Docstring Guidelines

- Use ScalaDoc format for public APIs
- Include parameter descriptions, return value explanations, and example usage
- Document pre-conditions, post-conditions, and side effects
- Provide links to related concepts or external documentation

### Code Documentation

- Write self-documenting code through clear naming and structure
- Add inline comments for complex business logic or non-obvious algorithms
- Document architectural decisions and trade-offs in code comments
- Keep documentation close to the code it describes to maintain accuracy

## Security

### Secrets Management

- Never hardcode sensitive information in source code
- Use environment variables or secure configuration management for secrets
- Implement proper access controls for configuration and secret access

### Input Validation

- Validate and sanitize all external inputs at application boundaries to prevent injection attacks
- Use allowlist validation approaches rather than blocklist filtering
- Reject malformed input early with clear error messages

### Security Practices

- Implement principle of least privilege in code design
- Use secure defaults in configuration and initialization
- Keep dependencies updated and scan for known vulnerabilities
