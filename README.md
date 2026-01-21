# VS Code hadolint Extension

[![CI Status](https://github.com/tobiashochguertel/vscode-hadolint/workflows/CI/badge.svg)](https://github.com/tobiashochguertel/vscode-hadolint/actions)
[![Visual Studio Marketplace Version](https://img.shields.io/visual-studio-marketplace/v/TobiasHochguertel.hadolint)](https://marketplace.visualstudio.com/items?itemName=TobiasHochguertel.hadolint)
[![Visual Studio Marketplace Installs](https://img.shields.io/visual-studio-marketplace/i/TobiasHochguertel.hadolint)](https://marketplace.visualstudio.com/items?itemName=TobiasHochguertel.hadolint)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

> **Note**: This is an actively maintained fork of the [original vscode-hadolint extension](https://github.com/michaellzc/vscode-hadolint) by [Michael Lin](https://github.com/michaellzc). The original project is no longer actively maintained. This fork includes updated dependencies, modern tooling, and ongoing bug fixes.

Integrates [hadolint](https://github.com/hadolint/hadolint), a Dockerfile linter, into VS Code. Please check their [documentation](https://github.com/hadolint/hadolint).

The extension uses the `hadolint` binary installed on your system. If the binary is not in your `$PATH`, the extension will not work as expected.

## ✨ Features

- 🔍 Real-time linting of Dockerfiles
- 📝 Inline error and warning messages
- 🎨 Syntax highlighting for issues
- ⚙️ Configurable via `.hadolint.yaml`
- 🔧 Multi-root workspace support
- 🔗 Direct links to rule documentation

## 📸 Preview

[![https://gyazo.com/a701460ccdda13a1a449b2c3e8da40bc](https://i.gyazo.com/a701460ccdda13a1a449b2c3e8da40bc.gif)](https://gyazo.com/a701460ccdda13a1a449b2c3e8da40bc)

## 🚀 Get Started

### Installation

#### Install hadolint

**macOS (Homebrew)**

```bash
brew install hadolint
```

**Linux**

```bash
# Download binary
curl -L https://github.com/hadolint/hadolint/releases/latest/download/hadolint-Linux-x86_64 -o hadolint
chmod +x hadolint
sudo mv hadolint /usr/local/bin/
```

**Windows**
Download the latest Windows binary from the [release page](https://github.com/hadolint/hadolint/releases/latest).

#### Install Extension

1. Open VS Code
2. Press `Ctrl+P` / `Cmd+P`
3. Type `ext install TobiasHochguertel.hadolint`
4. Press Enter

Or install from the [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TobiasHochguertel.hadolint).

## ⚙️ Configuration

Configure the extension through VS Code settings:

```json
{
  "hadolint.hadolintPath": "hadolint",
  "hadolint.cliOptions": ["--no-color", "--ignore", "DL3000"],
  "hadolint.maxNumberOfProblems": 100,
  "hadolint.outputLevel": "warning"
}
```

### Configuration Options

| Option                         | Type   | Default          | Description                                      |
| ------------------------------ | ------ | ---------------- | ------------------------------------------------ |
| `hadolint.hadolintPath`        | string | `"hadolint"`     | Path to hadolint executable                      |
| `hadolint.cliOptions`          | array  | `["--no-color"]` | Additional CLI options                           |
| `hadolint.maxNumberOfProblems` | number | `100`            | Maximum number of problems to show               |
| `hadolint.outputLevel`         | string | `"warning"`      | Minimum severity level (error/warning/info/hint) |

### Project Configuration

Create a `.hadolint.yaml` file in your project root for project-specific rules:

```yaml
ignored:
  - DL3000
  - DL3008
trustedRegistries:
  - docker.io
  - ghcr.io
```

> **Note:** This extension is multi-root workspace compatible. Each folder can have its own `.hadolint.yaml` configuration.

Learn more about hadolint configuration in the [official documentation](https://github.com/hadolint/hadolint#configure).

## 🛠️ Development

### Prerequisites

- Node.js >= 18
- npm >= 9

### Setup

```bash
# Clone the repository
git clone https://github.com/tobiashochguertel/vscode-hadolint.git
cd vscode-hadolint

# Install dependencies
npm install

# Build the extension
npm run build
```

### Running in Development Mode

1. Open the project in VS Code
2. Press `F5` to launch the Extension Development Host
3. Open a Dockerfile to test

### Using Taskfile

This project uses [Taskfile](https://taskfile.dev) for task management:

```bash
# List available tasks
task

# Build the extension
task build

# Run tests
task test

# Package the extension
task package
```

### Local Workflow Testing with Act

This project includes support for testing GitHub Actions workflows locally using [nektos/act](https://github.com/nektos/act).

#### Install act

**macOS (Homebrew)**

```bash
brew install act
```

**Linux**

```bash
curl https://raw.githubusercontent.com/nektos/act/master/install.sh | sudo bash
```

**Windows (Chocolatey)**

```bash
choco install act-cli
```

Or use the automated installation task:

```bash
task act:install
```

#### Run Workflows Locally

```bash
# List available workflows
task act:list

# Run CI workflow
task act:ci

# Run only lint job
task act:ci:lint

# Run only test jobs
task act:ci:test

# Run CodeQL analysis
task act:codeql

# Dry-run all workflows
task act:dryrun
```

This allows you to test GitHub Actions workflows locally before pushing to the repository, catching issues early in the development cycle.

## 📝 License

MIT License - see [LICENSE](LICENSE) file for details.

## 👤 Maintainer

**Tobias Hochgürtel**

- GitHub: [@tobiashochguertel](https://github.com/tobiashochguertel)

## 🙏 Acknowledgments

- Original project by [Michael Lin](https://github.com/michaellzc)
- [hadolint](https://github.com/hadolint/hadolint) by the hadolint team

## 📊 Marketplace Badges Setup

The badges in this README require the extension to be published. Here's what you need:

1. **GitHub Actions Badge**: Already configured, will work automatically after pushing
2. **VS Code Marketplace Badges**: Will work after first publication to marketplace
3. To publish to VS Code Marketplace:
   - Create a [Personal Access Token (PAT)](https://code.visualstudio.com/api/working-with-extensions/publishing-extension#get-a-personal-access-token)
   - Add it as `VSCE_PAT` secret in GitHub repository settings
4. To publish to Open VSX:
   - Create an account at [open-vsx.org](https://open-vsx.org/)
   - Generate an access token
   - Add it as `OVSX_PAT` secret in GitHub repository settings
