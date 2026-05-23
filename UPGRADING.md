# Upgrading Amanda

This file describes how to upgrade Amanda from a previous version.

In general, upgrades are seamless. When an upgrade requires additional steps, they are documented here.

Follow the instructions in order for your version range.

## Upgrading to 3.6.0 (Consolidated Release)

Amanda 3.6.0 is a consolidated release that merges the 3.5 and 3.6 development branches. It includes all features from 3.6 plus all security fixes from 3.5.4.

### Before You Upgrade

1. **Back up your configuration** - copy `/etc/amanda/` and any custom configurations
2. **Back up your catalog** - export your Amanda catalog:
   ```bash
   amadmin YOUR_CONFIG export > catalog-backup.txt
   ```
3. **Note your current version** - run `amanda --version`

### Upgrade Steps

1. Build and install the new version (see [INSTALL.md](INSTALL.md))
2. Restart the Amanda services
3. Run `amcheck YOUR_CONFIG` to verify the configuration
4. Run a test backup to verify everything works

### Compatibility

- **3.5.x to 3.6.0** - Fully compatible. No catalog migration needed.
- **3.4.x to 3.6.0** - Compatible, but review your configuration for deprecated options.
- **Older versions** - See the legacy upgrade notes below.

### Notable Changes

- `amservice`, `amcheck`, `planner`, `dumper` are no longer SUID root. A new `ambind` utility handles privileged port binding.
- Autolabel is disabled by default for non-Amanda and other-config labels. If you relied on this behavior, re-enable it with the build flag.
- The REST API server now supports Unix sockets and stores its PID file in `/tmp/amanda`.
- Default streaming buffer for tapes has been raised to 128K.

## Upgrading from pre-2.4.0

Amanda 2.4.0 introduced a protocol incompatibility. Pre-2.4.0 clients and servers cannot interoperate with 2.4.0+ versions. Upgrade all clients and servers at the same time.

To test the new version alongside the old, use `--with-testing` during configure. This installs Amanda with alternate service names (`Amanda-test`).

### Database Migration

If your Amanda version used a different database library, export and re-import your catalog:

**Before upgrade (old version):**
```bash
cd /var/AMANDA/CONFIG
amadmin CONFIG export > zzz
mkdir backup
mv curinfo* backup
```

**After upgrade (new version):**
```bash
cd /var/AMANDA/CONFIG
amadmin CONFIG import < zzz
```

Remove the backup after you are satisfied with the new version:
```bash
cd /var/AMANDA/CONFIG
rm -rf backup
```

### Index Directory Change (2.4.0+)

After 2.4.0, the index directory structure changed from flat to three-level:

```
[indexdir]/hostname/filesystem/YYYYMMDD_L.gz
```

A migration script is available if needed.
