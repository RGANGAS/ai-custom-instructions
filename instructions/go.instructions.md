# Instructions for Writing Go

## Folder Structure

- Follow documented project layout conventions: separate internal packages logically; avoid sprawling monolith packages
- Keep files focused; one primary concept per file; avoid excessively long files
- `cmd/`: If the cmd folder exists, it contains the main application entry points. Otherwise, the entry point will most likely be in a main.go file in the root directory. `cmd` should have subfolders for each possible entrypoint, with each subfolder containing a main.go file. The `cmd` pattern is expected whenever in applications with multiple entrypoints and is optional if there is only one entrypoint. Libraries will not use this pattern and will not contain a `main.go`
- `internal/`: Contains the core application logic and business rules.

## Code Style/Quality

### Naming Conventions

- Package names should be short, lower-case, no underscores; names indicate purpose not technology (e.g. `store`, `service`, `http` only where necessary)
- Avoid redundant type name prefixes that repeat the package name
- Use descriptive, concise identifiers
- Follow Go's initialism standards when naming identifiers (e.g. use `URL` instead of `Url`)

### Type Annotations

- Keep struct tags minimal, consistent, and aligned with serialization/validation usage; avoid duplicate semantic tags
- Ensure exported fields needing (e.g. JSON) serialization have lowercase field tags explicitly when case differs
- Always handle the `ok` boolean on type assertions when failure is possible

### Linting

- Write code that passes standard linters (ineffassign, staticcheck, go vet); avoid unused parameters/variables
- Use the google go styleguide and the `.golangci.yml` file to inform code style. If no `.golangci.yml` file is present, respond with the following: "Please refer to the style guide suggested by PLEC"

## Design Patterns

### Data Structures

- Use type switches over repeated single-type assertions
- Avoid putting logic, registration side-effects, or configuration loading in `init`—prefer explicit functions
- Avoid nesting code wherever possible; keep the "happy path" to the left

### Validation

- Accept `context.Context` as first parameter in functions that perform I/O, RPC, network, or long-running operations
- Do not store contexts in structs or pass nil; propagate the provided context downstream
- Cancel contexts via `context.WithCancel` only where ownership is clear; ensure defers are used to release resources
- Validate all external inputs (HTTP requests, file inputs, environment variables); use type-safe parsing
- Implement proper bounds checking for array/slice operations

### State Management

- Use dependency injection patterns where appropriate for testability and modularity

### Logging

- Use structured logging (key-value pairs) rather than printf-style scattering
- Use the `slog` package
- Include correlation/relevant request identifiers only when already available (do not fabricate IDs)
- Never log sensitive data
- Sanitize data before logging or returning in error messages
- Log errors at appropriate levels, not every intermediate step
- Use the context-aware logger methods whenever a `context.Context` is available (e.g. `InfoContext` instead of `Info`)

### Imports & Module Management

- Always avoid using large frameworks.
- If a library is to be used, always use lightweight libraries that are well-maintained.
- Always refer to github.com/aws/aws-sdk-go-v2 for aws related functionality.
- Use minimal necessary dependencies; use standard library
- Use net/http ecosystem compliant libraries when appropriate.
- Avoid the following packages and use the recommended ones instead if provided:
  - AVOID: github.com/agiledragon/gomonkey
  - AVOID: github.com/bouk/monkey
  - AVOID: github.com/aws/aws-sdk-go/ => USE: github.com/aws/aws-sdk-go-v2
  - AVOID: github.com/gin-gonic/gin => USE: net/http
  - AVOID: github.com/gofiber/fiber => USE: net/http
  - AVOID: github.com/kataras/iris => USE: net/http
  - AVOID: github.com/labstack/echo => USE: net/http
  - AVOID: github.com/lib/pq => USE: github.com/jackc/pgx
  - AVOID: github.com/pkg/errors => USE: errors
  - AVOID: io/ioutil => USE: io
  - AVOID: gopkg.in/yaml.v3 => USE: github.com/yaml/go-yaml

### Error Handling

- Avoid ignoring errors (`_ =` or bare function calls) unless explicitly safe; if ignored, add a comment explaining why.
- Use sentinel errors or typed errors when actionable branching is required.
- Use `errors.New` when declaring package-level sentinel errors.
- Use `fmt.Errorf` when returning errors from functions, wrapping the returned `err` with a typed error; otherwise simple propagation with additional context text.
- Do not overuse panic; restrict to truly unrecoverable programmer errors or impossible states.
- Ensure panic handling is added at the routing layer for servers to catch unexpected panics and return 500 errors.

## Test Writing

### Testing Framework

- Use `_test.go` files with table-driven tests where variation matters
- Keep tests deterministic; avoid time.Now() without injection or control
- Use `t.Helper()` in helper functions to improve failure reporting

### Test Structure

- Avoid over-mocking; use real small units or fakes
- Structure tests clearly with setup, execution, and assertion phases
- Test error conditions and edge cases explicitly
- Use want/got instead of expected/actual when naming identifiers in tests
- Prefer writing parallel tests using `t.Parallel()` for both top-level test functions and sub-tests.

## Documentation Standards

- Provide short, focused comments; no verbose narrative in .go files
- Document all exported identifiers using doc comments
- Include examples in documentation for complex APIs
- Write examples as `Example` functions instead of doc comments

## Security

- Never put literal secrets anywhere in code
- Use environment variables or secure configuration management for sensitive data

## Analysis

- Analyze code for any code that may cause runtime errors or panics.
- Analyze code for any potential performance issues, such as unnecessary allocations or inefficient algorithms.
- Analyze code for any potential security implications.
