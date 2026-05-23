# Agent Rules

## Remote Safety
- NEVER push to `origin` (zmanda/amanda). All pushes go to `konidev` (konidev20/amanda) only.
- `origin` is the upstream zmanda/amanda repo -- read-only.
- `konidev` is the working fork -- all branch creation and pushes target this remote.

## Build & Test
- Build system: Autotools (`./autogen && ./configure && make`)
- Test suite: `make installcheck` (Perl-based test harness in `installcheck/`)
- Languages: C, Perl, m4, Shell

## Branching
- `3_5` (from origin) is the current stable release branch (v3.5.4)
- `main` on konidev is the new development trunk (reset from 3_5, targeting 3.6.0)
- Feature branches should be created from `main`
