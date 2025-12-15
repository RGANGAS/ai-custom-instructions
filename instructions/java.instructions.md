# Instructions for Writing Java

## Code Standards

- Use consistent package naming: com.companyname.<line-of-business>.<organization>.<component-name> (UK variants: com.companyname.uk.<component-name> or uk.co.companyname.services.<component-name>).
- Use final keyword liberally for classes that should not be subclassed, methods not intended for override, and fields/locals that should not change.
- Wrap primitive identifiers (e.g., AccountId) to prevent accidental misuse of raw strings.
- Use enums for fixed sets rather than strings.
- Favor strong domain types (value objects) rather than primitive/string soup.
- Combine nested `if` statement in `else` block to `else if` when possible
- Simplify boolean `if`/`else` to single return if possible
- Convert if else chain to switch when possible
- Use uppercase for long literal suffixes
- Simplify lambda syntax to method reference when possible
- Use `instanceof` instead of `Class.isInstance`
- Use pattern matching for instanceof instead of manually casting
- Convert functional interface instances to use lambda instead of anonymous classes
- Use `String.join` when possible
- Convert fields to local variables if their use is only local
- Make inner classes static where possible
- Replace string concatenation with string builder
- Precompile reused regular expressions
- Avoid object equality on null objects
- Avoid double negation
- Create array with curly brace if possible
- Convert loop into if when possible
- Raise embedded `if` into parent `if` when possible

## Formatting

- Defer to Google Java Style Guide (https://google.github.io/styleguide/javaguide.html).
- Emit fully formatted, compilable Java with proper package, imports, and no unused imports.
- Use meaningful domain-centric names (IdentityFactory over UUIDGenerator).

## Design Patterns

- Organize code by clean architecture layers (config, repository, consumer, producer, client, job, domain, web). Place new classes in the appropriate layer.
- Use immutable objects; model data with records (Java 16+).
- Construct objects fully via constructor or builder; avoid multi-step mutation sequences.
- Use records for simple immutable aggregates where equals/hashCode/toString semantics match desired behavior.
- For complex construction with optional parameters, generate a builder that produces an immutable instance (no mutators post-build).
- Prevent partially-initialized states; enforce invariants at construction time.
- Use Optional over null; use immutable collections where feasible.
- Return Optional<T> instead of nullable references when absence is a valid outcome and no natural empty value exists.
- Prefer empty collections/objects over null for multi-value results.
- For mutable collaborators passed in (collections), perform defensive copies where needed.
- Use defensive copying or unmodifiable views when exposing internal collections.
- Represent money and currency with appropriate domain model (not floating point primitives).
- Keep domain layer free of framework annotations where possible.

## Validation

- Validate all inputs at entry points using appropriate validation frameworks.
- Use Jakarta Bean Validation annotations on request DTOs for complex validation.

## Error Handling

- Throw early (validate inputs up front) and catch late at a contextual boundary (controller advice, top-level flow) unless local recovery is possible.
- Use specific exception types; descriptive messages conveying failing operation and key identifiers.
- Use try-with-resources for AutoCloseable resources instead of manual finally blocks.
- Use structured logging instead of printing stack traces directly to stdout/stderr.
- Maintain an error catalog (externalized codes/messages) for consistency; map internal exceptions to standardized error responses.
- Centralize exception handling (e.g., controller advice) rather than duplicating try/catch in controllers.

## Test Writing

- Write unit tests for each public method and constructor.
- Structure tests with clear Arrange-Act-Assert patterns.
- Use appropriate test doubles (mocks, stubs) to isolate units under test.
- Write tests for edge cases and error conditions, not just happy paths.
- Keep each test method focused and independent.

## Documentation Standards

- Provide Javadoc for public types & methods (concise summary, param/return when non-obvious).
- Use SLF4J facade; use parameterized logging (logger.info("User {} created", id)).
- Use appropriate log levels: TRACE (deep detail), DEBUG (dev diagnostics), INFO (lifecycle & significant events), WARN (unexpected but tolerable), ERROR (recoverable failure), FATAL (abort-level critical).
- Choose Log4j2 or Logback backend as needed; do not mix multiple implementations.
- Document rationale for any dependency version overrides with CVE references.

## Security

- Never put literal secrets anywhere in code.
- Avoid logging sensitive data; restrict PII unless explicitly sanitized.
- Use secure coding practices for data handling and transmission.
- Implement proper authentication and authorization checks.
