# Changelog

All notable changes to this project will be documented in this file.

## [Unreleased] - 3.6.0-dev

### Consolidation

The Amanda 3.5 and 3.6 development branches have been consolidated into a single `main` branch. This release combines:

- Advanced features from the 3.6 development branch
- Security and stability fixes from 3.5.4
- S3 device overhaul
- NDMP improvements
- Gnulib upgrade to version 37
- All CVE fixes from 3.5.4

### Added

- REST API server with Unix socket support
- `amvault` `--uniq`, `--no-uniq`, `--delayed`, `--run-delayed` options
- `amstatus` `--[no]taped` argument
- `amdump` `--no-dump`, `--no-flush`, `--no-vault` arguments
- `ampgsql` `--incremental`, `--remove-full-wal`, `--remove-incremental-wal` properties
- `ambind` privileged port binding utility
- `amanda-security.conf` with `tcp_port_range` and `udp_port_range`
- OpenStack Keystone v3 support for S3 device
- Diskflat device driver
- Better thread naming in debug logs

### Changed

- Default REST API port set to 5000
- `amfetchdump` `--directory` renamed to `--target`
- `amvault` default behavior is now `--uniq`
- `amservice`, `amcheck`, `planner`, `dumper` are no longer SUID root
- Autolabel disabled by default for non-Amanda and other-config labels
- Minimum streaming buffer for tapes raised to 128K
- Self-test search paths changed from `/usr/bin` to `/bin`

### Fixed

- CVE-2022-37703: Directory existence disclosure via perror in calcsize SUID binary
- CVE-2022-37704: Privilege escalation via RSH environment in rundump
- CVE-2022-37705: Argument checking in runtar
- CVE-2023-30547: Privilege escalation via calcsize SUID binary
- CVE-2023-30577: Argument checking in runtar
- IPv6 address handling in security and socket utilities
- JSON parsing of numbers like `0.0` and `3.0`
- Double-posting cancel of shm_ring
- Crash when `log_file` global is NULL
- Holding privileged group IDs after setuid drop
- IPv6 localhost detection
- Configuration file include error messages
- Compilation on Solaris, FreeBSD, OpenBSD
- Planner looping issue
- S3 device overflow
- Race condition in amarchive reader
- amrecover hang
- amvault segfault
- SO-GIS compliant key derivation
- Suppressed first character of error message in bsdtcp-security
- Post-install script amkey creation
- jQuery vulnerability (removed obsolete dependency)

### Removed

- Obsolete jQuery dependency from web interface

---

## [3.5.2] - Previous Release

### Added

- `amstatus` `--[no]taped` argument
- `amvault` `--uniq`, `--no-uniq`, `--delayed`, `--run-delayed` arguments

## [3.5.1] - Previous Release

### Fixed

- Compilation on Solaris
- SUID binary `r` bit check
- Configuration override (`-o`) parsing
- Client shared memory availability check
- `amreport` improvements
- Datestamp wildcard (`*`) support
- Holding disk lock for parallel access protection

## [3.5] - Previous Release

### Added

- Threaded client connections
- `ambind` SUID program for privileged port binding
- `amanda-security.conf` with port range configuration
- OpenStack Keystone v3 support for S3
- `ampgsql` incremental and WAL removal properties

### Changed

- `amfetchdump` `--directory` renamed to `--target`
- `amservice`, `amcheck`, `planner`, `dumper` no longer SUID root

---

For detailed historical changes, see [NEWS](NEWS) and [ChangeLog](ChangeLog).
