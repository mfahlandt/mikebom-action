# Security Policy

## Supported Versions

| Version | Supported          |
| ------- | ------------------ |
| latest  | :white_check_mark: |

## Reporting a Vulnerability

If you discover a security vulnerability in this project, please report it
responsibly:

1. **Do NOT open a public GitHub issue.**
2. Email the maintainer at the address listed in the GitHub profile, or use
   [GitHub's private vulnerability reporting](https://docs.github.com/en/code-security/security-advisories/guidance-on-reporting-and-writing/privately-reporting-a-security-vulnerability).
3. Include:
   - A description of the vulnerability
   - Steps to reproduce
   - Potential impact
   - Suggested fix (if any)

We will acknowledge receipt within 48 hours and aim to release a fix within
7 days for critical issues.

## Security Best Practices in This Action

- All third-party actions are pinned by full SHA commit hash
- The mikebom binary is verified against published SHA256 checksums
- The action requests minimal permissions (`contents: read`)
- Dependabot is configured to keep dependencies up to date
- OpenSSF Scorecard runs weekly to monitor security posture

