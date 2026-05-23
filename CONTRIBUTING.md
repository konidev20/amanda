# Contributing to Amanda

Thank you for your interest in contributing to Amanda! This project has been maintained by the community for over 30 years, and we welcome new contributors.

## Getting Started

### 1. Fork and Clone

```bash
git clone git@github.com:YOUR_USERNAME/amanda.git
cd amanda
git remote add upstream git@github.com:konidev20/amanda.git
```

### 2. Build and Test

```bash
./autogen
./configure
make
make installcheck
```

See [INSTALL.md](INSTALL.md) for full build instructions and prerequisites.

## Branching Model

- **`main`** - the active development branch, targeting Amanda 3.6.0
- **Feature branches** - create from `main`, name them descriptively (e.g., `fix-s3-upload-hang`)
- **`3_5`** - the legacy stable branch on the upstream repo (read-only)

All development happens on `main`. Create feature branches from it and submit pull requests back to `main`.

## Submitting Changes

1. Create a branch from `main`
2. Make your changes
3. Run the test suite: `make installcheck`
4. Commit with a clear message (see below)
5. Push to your fork and open a Pull Request

### Commit Messages

Use a short summary line, then a blank line, then details if needed:

```
fix: correct S3 multipart upload retry logic

The retry counter was not being reset between parts,
causing uploads to fail after the first retry.
```

Prefix suggestions:
- `fix:` - bug fixes
- `feat:` - new features
- `docs:` - documentation changes
- `build:` - build system changes
- `test:` - test suite changes
- `chore:` - maintenance tasks

## Code Style

### C Code

- Use K&R style with braces on the same line for functions
- Indent with 4 spaces (no tabs)
- Wrap lines at 80 characters where practical
- Follow existing patterns in the codebase

### Perl Code

- Use `use strict;` and `use warnings;`
- Follow existing patterns in `perl/Amanda/`

### Shell Scripts

- Use `#!/bin/sh` unless bash-specific features are needed
- Quote all variable expansions

## Reporting Bugs

Use [GitHub Issues](https://github.com/konidev20/amanda/issues). Include:

- Amanda version
- Operating system and version
- Steps to reproduce
- Expected vs actual behavior
- Relevant log output (from `/var/log/amanda/`)

## Reporting Security Issues

See [SECURITY.md](SECURITY.md) for the responsible disclosure process.

## Getting Help

- **Mailing lists** - [amanda.org/support/mailinglists.php](http://www.amanda.org/support/mailinglists.php)
- **amanda-hackers** - for development discussion
- **amanda-users** - for user questions

## Areas That Need Help

We're especially looking for help with:

- Packaging (deb, rpm) for modern distributions
- Documentation updates
- Test coverage improvements
- Build system modernization
- Bug triage and reproduction

Thank you for contributing!
