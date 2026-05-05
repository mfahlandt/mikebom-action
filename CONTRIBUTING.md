# Contributing to mikebom-action

Thank you for your interest in contributing! This document provides guidelines
for contributing to this project.

## How to Contribute

1. **Fork** the repository
2. **Create a branch** for your feature or fix (`git checkout -b feature/my-feature`)
3. **Make changes** and ensure tests pass
4. **Sign your commits** using DCO sign-off (`git commit -s`)
5. **Push** to your fork and open a **Pull Request**

## Developer Certificate of Origin (DCO)

All contributions must be signed off per the
[DCO](https://developercertificate.org/). Add `-s` to your git commit:

```bash
git commit -s -m "feat: add new feature"
```

## Local Testing

You can test the action locally by running the script directly:

```bash
export INPUT_PATH="."
export INPUT_FORMAT="cyclonedx-json"
export INPUT_OUTPUT_FILE="test-sbom.json"
export INPUT_MIKEBOM_VERSION="v0.1.0-alpha.14"
export INPUT_INCLUDE_DEV="false"
export INPUT_OFFLINE="false"
export INPUT_IMAGE=""
export INPUT_IMAGE_SRC=""
export GITHUB_OUTPUT="/dev/null"
export RUNNER_TEMP="/tmp"

bash scripts/run.sh
```

## Code Style

- Shell scripts must pass [ShellCheck](https://www.shellcheck.net/)
- YAML files should be valid and follow the existing style
- Use meaningful commit messages following
  [Conventional Commits](https://www.conventionalcommits.org/)

## Reporting Issues

- Use GitHub Issues for bug reports and feature requests
- For security vulnerabilities, see [SECURITY.md](SECURITY.md)

## License

By contributing, you agree that your contributions will be licensed under the
Apache License 2.0.

