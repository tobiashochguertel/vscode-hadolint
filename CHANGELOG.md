# Change Log

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](http://keepachangelog.com/)
and this project adheres to [Semantic Versioning](http://semver.org/).

## [Unreleased]

## [2.0.0] - 2026-01-21

### Breaking Changes

- Updated to require VS Code >= 1.85.0
- Updated to require Node.js >= 18

### Added

- Comprehensive Taskfile.yml for project maintenance and release automation
- GitHub Actions CI/CD workflows for automated testing and publishing
- Support for publishing to both VS Code Marketplace and Open VSX Registry
- Modern GitHub Actions workflows replacing Travis CI
- Repository topics for better discoverability
- Enhanced README with installation instructions and badge setup guide
- New maintainer: Tobias Hochgürtel

### Changed

- Renamed default branch from `master` to `main`
- Updated all dependencies to latest stable versions:
  - TypeScript 4.5.5 → 5.7.3
  - esbuild 0.12.1 → 0.24.2
  - mocha 8.4.0 → 11.7.5
  - vscode-languageclient 8.0.2 → 9.0.1
  - vscode-languageserver 8.0.2 → 9.0.1
  - @vscode/test-electron (replacing deprecated vscode-test)
  - @vscode/vsce (replacing deprecated vsce)
- Modernized package.json with proper author information and repository links
- Updated LICENSE to acknowledge both original and current maintainer
- Improved README documentation with features, configuration table, and development guide
- Removed deprecated activation event for commands

### Fixed

- Security vulnerabilities in dependencies
- Removed rome dependency (deprecated project)
- Updated CI to test on macOS, Linux, and Windows

### Infrastructure

- Migrated CI from Travis to GitHub Actions
- Added automated release workflow with tag-based deployment
- Set up automated package versioning with Taskfile

## [1.1.2] - 2022-08-06

### Fixed

- Handle an edge case of showing spammy error message

## [1.1.1] - 2022-02-26

### Changed

- Bump various dependencies

## [1.1.0] - 2021-07-09

### Added

- Reference link to lint rule documentation

## [1.0.2] - 2021-03-27

### Fixed

- Graceful handling of the upstream colorized output feature
- Revalidate on file save

## [1.0.1] - 2021-02-15

### Changed

- Optimized extension production build with webpack

## [1.0.0] - 2021-02-14

### Added

- Multi-root workspae support

## [0.3.0] - 2018-12-01

### Added

- Revalidate all Dockerfile when `.hadolint.yaml` is changed

## [0.2.3] - 2018-11-28

### Changed

- Upgrade dependencies

## [0.2.2] - 2018-11-08

### Fixed

- Revalidate Dockerfile now works on file saved

## [0.2.1] - 2018-09-22

### Fixed

- Fixed broken Dockerfile fs path on win32

### Changed

- Add instruction for win32 users to setup path to hadolint excutable

## [0.2.0] - 2018-05-30

### Added

- Add optiont to set custom full path to hadolint executable

## [0.1.1] - 2018-04-23

### Fixed

- Add missing output level configuration

## [0.1.0] - 2018-04-22

### Added

- Add option to set default output level

## [0.0.3] - 2018-04-20

### Changed

- Improve npm build scripts
- Update development instruction

### Fixed

- Fixed window error message typo

## [0.0.2] - 2018-04-20

### Fixed

- Fix broken tsconfig
- Fix broken npm script type: should use yarn over npm

## [0.0.1] - 2018-04-19

### Added

- First release
