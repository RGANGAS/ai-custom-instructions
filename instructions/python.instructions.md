# Instructions for Writing Python

## Dependency Handling

- Use virtual environment patterns (.venv) for all dependency management; never hardcode global `site-packages` paths
- Use only `pipenv` for installing and upgrading Python libraries or dependencies. Use Pipfile and Pipfile.lock.
- If there is a problem with a native extension dependency (e.g., an error about glibc) suggest upgrading that dependency

# Imports

- Only do imports at the module level. Avoid lazy runtime imports.
- Never use wildcard imports.

## Project Configuration

- Follow PEP 621 and use pyproject.toml for project setup, build system definitions, library dependency requirements, and tool configuration including ruff, black, mypy, and pytest
- Add ruff configuration to pyproject.toml if not present.

## Code Standards

- Prefer conservative, standards-aligned implementation over clever meta-programming
- Keep module top-level side effects minimal (define functions/classes; guard runtime code with `if __name__ == "__main__"`)
- Replace magic numbers/strings with named constants (ALL_CAPS) optionally typed Final
- Module-level variables must be immutable.

### Naming Conventions

- Avoid abbreviations unless they are widely understood

### Type Annotations

- Always include type hints for all code you write.
- Use modern syntax (list[str], dict[str, Any], X | Y) instead of typing.List/Union
- Use `T | None` instead of `Optional[T]`
- Avoid over-nesting complex generic types. Use TypedDict or dataclass if types get complex.
- Never silence type errors with broad `# type: ignore` without a reason comment (e.g. `# type: ignore[attr-defined]  # third-party stub missing attr`)
- Suggest stub (.pyi) creation or types-\* package when an external library lacks types instead of removing annotations

## Formatting

- Follow PEP 8 and PEP 257 (docstrings)
- Format code in the same way `black` would format code.

## Design Patterns

- Use dataclasses for structured data instead of loosely typed dicts; prefer `@dataclass(frozen=True)` for immutable value objects
- Use Literal sparingly; prefer Enum for enumerations of many fixed values
- Favor pure functions and immutable dataclasses for deterministic behavior and easier testing
- Prefer python native methods vs. shelling out to subprocesses for core logic

## Validation

- Validate and sanitize external data at the external boundaries of the program (HTTP inputs, API responses, secrets retrieval, user input) and then treat internal objects as trusted. Only use Pydantic models at those external boundaries, not for internal trivial value passing.
- After Pydantic validation, rely on static type safety. Avoid redundant isinstance checks.

## Error Handling

- When catching broad exceptions around dependency imports, re-raise with an actionable message rather than pass
- Always catch specific exception types, never Exception or Error.
- Avoid swallowing ValidationError/TypeError silently
- Log errors appropriately with sufficient context for debugging

## Test Writing

- Default to pytest for unit test authoring unless `unittest` is already imported
- Type annotate test helpers; keep fixtures minimal
- Structure tests with clear arrange/act/assert patterns
- Write tests for edge cases and error conditions, not just happy paths
- Keep each test method focused and independent

## Documentation

- Auto-generate concise docstrings: first line summary, blank line, param/return descriptions only if non-trivial
- Never include the type of a param or return value in the docstring
- For dataclasses, include a class docstring summarizing purpose and invariants when helpful
- Keep comments and documentation up-to-date when you change code
- Update README with usage examples and setup instructions when necessary
- Only include comments that explain why code was written. Avoid describing what code is doing in comments.

## Security

- Never put literal secrets anywhere in code.
- Retrieve secrets only via a library or environment variables already populated
- Use secure defaults for cryptographic operations
