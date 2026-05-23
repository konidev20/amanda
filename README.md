# Amanda

**The Advanced Maryland Automatic Network Disk Archiver**

Amanda is an open-source backup system designed to back up multiple computers on a network to disk, tape, or cloud storage. It has been in active development since 1991 at the University of Maryland.

## What Amanda Does

Amanda backs up your servers and workstations using standard Unix tools (`dump`, `tar`, etc.) and stores the backups on:

- **Disk** (holding disk, NAS, SAN)
- **Tape** (LTO, DLT, DAT, tape libraries)
- **Cloud** (Amazon S3 and compatible storage)

It schedules full and incremental backups automatically, manages your tape inventory, and tells you exactly which tape you need for a restore.

## Key Features

- **Parallel backups** - backs up multiple clients simultaneously to a holding disk, then writes to tape/cloud sequentially
- **Multiple storage backends** - disk, tape changers, Amazon S3, NDMP
- **Secure transport** - SSH, Kerberos 5, or BSD authentication
- **Encryption** - GPG or custom encryption on client or server
- **Compression** - gzip, compress, or custom programs
- **Application support** - PostgreSQL, MySQL, Samba, and custom backup plugins
- **REST API** - manage Amanda programmatically
- **IPv6 support**
- **Spanning** - large backups automatically span multiple tapes
- **Pre/post scripts** - run custom commands before and after backups

## Quick Start

### Build from Source

```bash
./autogen
./configure
make
sudo make install
```

See [INSTALL.md](INSTALL.md) for detailed build instructions and prerequisites.

### Requirements

- C compiler (GCC recommended)
- GLib 2.x development libraries
- Perl 5.x with standard modules
- GNU make, autoconf, automake, libtool
- Optional: `libcurl` (S3 support), `libpq` (PostgreSQL), `gnutls`/`openssl` (encryption)

## Documentation

- **Installation guide** - [INSTALL.md](INSTALL.md)
- **What's new** - [NEWS](NEWS)
- **Changelog** - [CHANGELOG.md](CHANGELOG.md)
- **Upgrade guide** - [UPGRADING.md](UPGRADING.md)
- **Man pages** - installed with `make install` in section 8 and 5
- **Sample configurations** - see the `example/` directory

## Contributing

Contributions are welcome! Amanda has been community-maintained for over 30 years.

- Read [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines
- Report bugs via [GitHub Issues](https://github.com/konidev20/amanda/issues)
- Discuss on the mailing lists (see below)

## Project Status

In 2023, the Amanda 3.5 and 3.6 development branches were consolidated into a single `main` branch. This release combines the advanced features of 3.6 with the security and stability fixes from 3.5.4, including:

- S3 device overhaul
- NDMP improvements
- Gnulib upgrade
- CVE fixes (CVE-2022-37703, CVE-2022-37704, CVE-2023-30547)

The project is now targeting **Amanda 3.6.0** as the next release from the consolidated codebase. We're looking for community members to help maintain and develop Amanda going forward.

## Support

- **GitHub Issues** - [Report bugs and request features](https://github.com/konidev20/amanda/issues)
- **Mailing lists** - [amanda.org/support/mailinglists.php](http://www.amanda.org/support/mailinglists.php)
  - `amanda-announce` - release announcements
  - `amanda-users` - user questions and discussion
  - `amanda-hackers` - development discussion

## License

Amanda is distributed under the University of Maryland BSD-style license and GPL. See [COPYRIGHT](COPYRIGHT) for details.

## Acknowledgments

Amanda was created at the University of Maryland and has been contributed to by dozens of developers over three decades. See [AUTHORS](AUTHORS) for a full list.
