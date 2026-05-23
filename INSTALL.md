# Installing Amanda

This guide covers building and installing Amanda from source.

## Prerequisites

### Build Dependencies

You will need the following packages to build Amanda:

**Debian/Ubuntu:**
```bash
apt-get install build-essential autoconf automake libtool \
  pkg-config libglib2.0-dev libcurl4-openssl-dev \
  libgnutls28-dev libpq-dev perl
```

**RHEL/CentOS/Fedora:**
```bash
dnf install gcc make autoconf automake libtool \
  pkg-config glib2-devel libcurl-devel gnutls-devel \
  postgresql-devel perl
```

**FreeBSD:**
```bash
pkg install gmake autoconf automake libtool \
  pkgconf glib2 curl gnutls postgresql15-client perl5
```

### Runtime Requirements

- **GLib 2.x** - core utility library
- **Perl 5.x** - required for server-side components and test suite
- **GNU tar** or **dump** - for performing backups
- **xinetd** or **systemd** - for running the Amanda daemon

### Optional Dependencies

| Feature | Package |
|---------|---------|
| S3/Cloud storage | libcurl |
| PostgreSQL backup | libpq |
| Encryption | gnutls or openssl |
| NDMP support | (built-in, no extra deps) |
| REST API server | Perl Dancer2, Starman |

## Create the Amanda User

Amanda runs as a dedicated user. Create one before installing:

```bash
sudo groupadd amanda
sudo useradd -g amanda -m -s /bin/bash amanda
```

## Build Amanda

```bash
./autogen
./configure
make
```

### Configure Options

Common options you may want to use:

| Option | Description |
|--------|-------------|
| `--prefix=/usr/local` | Installation prefix (default: `/usr/local`) |
| `--with-user=amanda` | Amanda daemon user (default: `amanda`) |
| `--with-group=amanda` | Amanda daemon group (default: `amanda`) |
| `--with-config=YOUR_CONFIG` | Default configuration name |
| `--with-holdingdisk` | Enable holding disk support (recommended) |
| `--with-gnutls` | Use GnuTLS for encryption |
| `--with-openssl` | Use OpenSSL for encryption |
| `--with-curl` | Enable S3/cloud storage support |
| `--with-postgresql` | Enable PostgreSQL backup support |
| `--without-rest-server` | Disable the REST API server |
| `--without-ndmp` | Disable NDMP support |
| `--with-static-binaries` | Build static binaries |
| `--with-amperldir=PATH` | Path to Amanda Perl modules |

Run `./configure --help` for the full list of options.

### Example Configuration

```bash
./autogen
./configure \
  --prefix=/usr/local \
  --with-user=amanda \
  --with-group=amanda \
  --with-gnutls \
  --with-curl \
  --with-postgresql
make
```

## Install

```bash
sudo make install
```

This installs binaries, libraries, man pages, and example configurations.

## Run the Test Suite

After installation, you can run the test suite:

```bash
make installcheck
```

This requires Amanda to be installed. The tests run in a temporary directory and do not affect your system.

## Post-Installation Setup

### 1. Set Up Directories

```bash
sudo mkdir -p /var/log/amanda
sudo mkdir -p /etc/amanda
sudo chown -R amanda:amanda /var/log/amanda
sudo chown -R amanda:amanda /etc/amanda
```

### 2. Configure the Amanda Daemon

Copy the example configuration:

```bash
sudo cp -r /usr/local/etc/amanda/example/ /etc/amanda/
```

Edit `/etc/amanda/amanda.conf` to match your setup. See the `example/` directory for sample configurations.

### 3. Set Up xinetd or systemd

**xinetd:** Copy the example xinetd configuration from `example/` to `/etc/xinetd.d/amanda`.

**systemd:** Use the example systemd unit files from `example/systemd/`.

### 4. Create a Backup Configuration

Create a configuration directory for your backup set:

```bash
sudo mkdir -p /etc/amanda/MyConfig
sudo cp /etc/amanda/example/amanda.conf /etc/amanda/MyConfig/
sudo cp /etc/amanda/example/disklist /etc/amanda/MyConfig/
```

Edit these files to define what to back up and where.

### 5. Set Up the Holding Disk

Amanda works best with a holding disk. This is a large partition used to buffer backups before writing to tape or cloud:

```bash
sudo mkdir -p /data/amanda/holding
sudo chown amanda:amanda /data/amanda/holding
```

The holding disk should be larger than your largest single backup.

## Verify the Installation

Check that Amanda is working:

```bash
amanda --version
amcheck MyConfig
```

## Troubleshooting

### "configure: error: GLib not found"
Install the GLib development package (`libglib2.0-dev` on Debian, `glib2-devel` on RHEL).

### "configure: error: no acceptable C compiler found"
Install GCC (`build-essential` on Debian, `gcc` on RHEL).

### "amcheck: command not found"
Make sure `/usr/local/sbin` is in your PATH, or use the full path.

### Permission errors
Ensure the amanda user owns the relevant directories and that file permissions are set correctly.

## Next Steps

- Read the man pages: `man amanda`, `man amanda.conf`, `man disklist`
- See [UPGRADING.md](UPGRADING.md) if upgrading from an older version
- Check [CONTRIBUTING.md](CONTRIBUTING.md) if you want to help develop Amanda
