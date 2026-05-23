# Notes for Developers

This document covers the basics of working with the Amanda codebase.

## Build System

Amanda uses Autotools (autoconf, automake, libtool) with Gnulib for portability.

```bash
./autogen          # Generate configure script
./configure        # Configure for your system
make               # Build
make installcheck  # Run test suite (requires install)
```

## Directory Structure

| Directory | Contents |
|-----------|----------|
| `common-src/` | Shared C library (security, protocol, utilities) |
| `client-src/` | Client-side code (sendbackup, sendsize, rundump, runtar) |
| `server-src/` | Server-side code (driver, dumper, planner, amvault) |
| `device-src/` | Device API (tape, file, S3, NDMP, diskflat) |
| `amandad-src/` | Amanda daemon |
| `xfer-src/` | Transfer API |
| `ndmp-src/` | NDMP protocol support |
| `application-src/` | Application plugins (amgtar, amstar, amsamba, ampgsql) |
| `perl/Amanda/` | Perl modules |
| `rest-server/` | REST API server (Perl/Dancer2) |
| `installcheck/` | Test suite (Perl-based) |
| `config/` | M4 macros, Gnulib, automake fragments |
| `example/` | Sample configurations |
| `packaging/` | Build scripts for deb, rpm, tar |

## Updating Gnulib

Gnulib should be updated periodically for compatibility with newer systems.

1. Clone gnulib:
   ```bash
   git clone https://git.savannah.gnu.org/git/gnulib.git /tmp/gnulib
   ```

2. Run the regenerate script from the Amanda root:
   ```bash
   GNULIB_TOOL=/tmp/gnulib/gnulib-tool ./gnulib/regenerate/regenerate
   ```

3. Review changes, test the build, and commit.

4. Update the gnulib commit reference in `gnulib/regenerate/regenerate`.

## Updating Libtool

```bash
libtoolize --force --copy
```

Review changes with `git status`, test, and commit.

## Updating Gettext

```bash
po/reautopoint
```

Review changes, test, and commit.

## Testing

The test suite lives in `installcheck/` and is run with:

```bash
make installcheck
```

Tests require Amanda to be installed. They run in a temporary directory and do not affect your system.

## Coding Conventions

- **C**: K&R style, 4-space indentation, follow existing patterns
- **Perl**: `use strict; use warnings;`, follow `perl/Amanda/` patterns
- **Shell**: POSIX sh unless bash is required

## Commit Messages

Use a prefix and short summary:

```
fix: correct S3 multipart upload retry logic
feat: add --delayed option to amvault
docs: update installation guide
```
