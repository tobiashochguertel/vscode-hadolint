# Contributing to vscode-hadolint

Thank you for your interest in contributing to vscode-hadolint! This document provides guidelines and information for contributors.

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [Getting Started](#getting-started)
- [Development Workflow](#development-workflow)
- [Testing](#testing)
- [Code Style](#code-style)
- [Submitting Changes](#submitting-changes)
- [Release Process](#release-process)

## Code of Conduct

Be respectful, inclusive, and professional. Harassment and discrimination will not be tolerated.

## Getting Started

### Prerequisites

- Node.js >= 18
- npm >= 9
- VS Code >= 1.85.0
- Git
- hadolint (for testing)

### Installation

```bash
# Clone the repository
git clone https://github.com/tobiashochguertel/vscode-hadolint.git
cd vscode-hadolint

# Install dependencies
npm install

# Or use Taskfile
task install
```

### Project Structure

```
vscode-hadolint/
├── client/              # VS Code extension client
│   ├── src/
│   │   ├── extension.ts           # Main entry point
│   │   └── command/               # Commands
│   └── package.json
├── server/              # Language Server
│   ├── src/
│   │   ├── server.ts              # LSP server
│   │   └── service/               # Services
│   └── package.json
├── .github/             # CI/CD workflows
├── docs/                # Documentation
└── Taskfile.yml         # Task automation
```

## Development Workflow

### Using Taskfile (Recommended)

```bash
# List all available tasks
task

# Build the extension
task build

# Watch for changes
task watch

# Run tests
task test

# Package extension
task package
```

### Using npm Scripts

```bash
# Compile TypeScript
npm run compile

# Build with esbuild
npm run build

# Watch mode
npm run watch

# Run tests
npm test
```

### Debugging

1. Open the project in VS Code
2. Press `F5` or select `Run > Start Debugging`
3. A new VS Code window will open with the extension loaded
4. Open a Dockerfile to test the extension

### Making Changes

1. Create a new branch:

   ```bash
   git checkout -b feature/your-feature-name
   ```

2. Make your changes

3. Build and test:

   ```bash
   task build
   task test
   ```

4. Commit your changes:
   ```bash
   git add .
   git commit -m "feat: add new feature"
   ```

## Testing

### Running Tests

**Important:** Close all VS Code instances before running tests.

```bash
# Run all tests
npm test

# Or with Taskfile
task test
```

### Writing Tests

We use Mocha for testing. Tests are located in `client/src/test/`.

**Example test:**

```typescript
import * as assert from "assert";
import * as vscode from "vscode";

suite("Extension Test Suite", () => {
  test("Extension should activate", async () => {
    const ext = vscode.extensions.getExtension("TobiasHochguertel.hadolint");
    assert.ok(ext);
    await ext?.activate();
    assert.ok(ext?.isActive);
  });
});
```

## Code Style

### TypeScript

- Use TypeScript strict mode
- Prefer `const` over `let`
- Use meaningful variable names
- Add JSDoc comments for public APIs

### Formatting

We don't currently use a formatter, but please:

- Use tabs for indentation
- Use single quotes for strings
- Add trailing commas in objects/arrays

### Naming Conventions

- **Files**: kebab-case (e.g., `select-executable.ts`)
- **Classes**: PascalCase (e.g., `LanguageClient`)
- **Functions**: camelCase (e.g., `validateTextDocument`)
- **Constants**: UPPER_SNAKE_CASE (e.g., `DEBUG_PORT_START`)

## Submitting Changes

### Commit Messages

Follow [Conventional Commits](https://www.conventionalcommits.org/):

```
feat: add new configuration option
fix: resolve issue with Windows paths
docs: update README with new examples
chore: update dependencies
test: add tests for hadolint service
refactor: extract configuration management
```

Types:

- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation only
- `style`: Formatting, missing semicolons, etc.
- `refactor`: Code restructuring
- `test`: Adding/updating tests
- `chore`: Maintenance tasks

### Pull Requests

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Update documentation if needed
6. Submit a pull request

**PR Title Format:**

```
feat: add support for .hadolintrc configuration
```

**PR Description Should Include:**

- What changed
- Why it changed
- How to test it
- Screenshots (if UI changes)
- Related issues

### Review Process

- All PRs require approval
- CI must pass
- Code must follow style guidelines
- Tests must pass

## Release Process

Releases are automated via GitHub Actions.

### Version Bump

```bash
# Patch (1.0.0 -> 1.0.1)
task version:patch

# Minor (1.0.0 -> 1.1.0)
task version:minor

# Major (1.0.0 -> 2.0.0)
task version:major
```

### Creating a Release

1. Update CHANGELOG.md
2. Bump version:
   ```bash
   task version:minor
   ```
3. Push to main:
   ```bash
   git push origin main
   ```
4. Create and push tag:
   ```bash
   git tag v1.2.0
   git push origin v1.2.0
   ```
5. GitHub Actions will automatically:
   - Run CI tests
   - Create GitHub release
   - Publish to VS Code Marketplace
   - Publish to Open VSX

### Manual Release (If Needed)

```bash
# Package
task package

# Publish to VS Code Marketplace
npx @vscode/vsce publish

# Publish to Open VSX
npx ovsx publish *.vsix -p $OVSX_PAT
```

## Getting Help

- **Issues**: [GitHub Issues](https://github.com/tobiashochguertel/vscode-hadolint/issues)
- **Discussions**: [GitHub Discussions](https://github.com/tobiashochguertel/vscode-hadolint/discussions)

## Resources

- [VS Code Extension API](https://code.visualstudio.com/api)
- [Language Server Protocol](https://microsoft.github.io/language-server-protocol/)
- [hadolint Documentation](https://github.com/hadolint/hadolint)
- [Taskfile Documentation](https://taskfile.dev)

## License

By contributing, you agree that your contributions will be licensed under the MIT License.
