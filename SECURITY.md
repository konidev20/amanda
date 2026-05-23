# Security Policy

## Supported Versions

| Version | Supported |
|---------|-----------|
| 3.6.x (main branch) | Yes |
| 3.5.x | Security fixes only (upstream) |
| Older versions | No |

## Reporting a Vulnerability

We take security seriously. If you discover a security vulnerability in Amanda:

1. **Do not** open a public GitHub issue
2. Email the maintainers at the address associated with this repository
3. Include:
   - A description of the vulnerability
   - Steps to reproduce
   - Potential impact
   - Any suggested fix (optional)

We will acknowledge your report within 48 hours and work with you to understand and fix the issue.

## Disclosure Process

1. Reporter submits vulnerability details privately
2. Maintainers confirm and assess severity
3. A fix is developed and tested
4. A new release is published with the fix
5. The vulnerability is publicly disclosed with credit to the reporter (if desired)

## Past Security Issues

| CVE | Description | Fixed In |
|-----|-------------|----------|
| CVE-2023-30547 | Privilege escalation via calcsize SUID binary | 3.5.4 |
| CVE-2023-30577 | Argument checking in runtar | 3.5.4 |
| CVE-2022-37704 | Privilege escalation via RSH environment in rundump | 3.5.4 |
| CVE-2022-37703 | Directory existence disclosure | 3.5.4 |
| CVE-2022-37705 | Argument checking in runtar | 3.5.4 |

## Security Best Practices

- Run the Amanda daemon as a dedicated `amanda` user, not root
- Use SSH or Kerberos for client-server communication
- Enable encryption for backup data in transit and at rest
- Keep your Amanda installation up to date
- Restrict access to Amanda configuration files and backup data
