# mikebom-action

[![CI](https://github.com/mfahlandt/mikebom-action/actions/workflows/ci.yml/badge.svg)](https://github.com/mfahlandt/mikebom-action/actions/workflows/ci.yml)
[![OpenSSF Scorecard](https://api.scorecard.dev/projects/github.com/mfahlandt/mikebom-action/badge)](https://scorecard.dev/viewer/?uri=github.com/mfahlandt/mikebom-action)
[![License: Apache-2.0](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)

A GitHub Action for generating Software Bill of Materials (SBOM) using
[mikebom](https://github.com/kusari-sandbox/mikebom) — a toolkit that produces
high-fidelity **CycloneDX 1.6**, **SPDX 2.3**, and **SPDX 3.0.1** SBOMs with
SHA-256 hashes, real dependency graphs, and evidence blocks.

## Features

- 🔍 **Source tree scanning** — scan any directory for dependencies
- 🐳 **Container image scanning** — scan OCI images (local docker or remote registry)
- 📦 **Multiple formats** — CycloneDX JSON, SPDX 2.3 JSON, SPDX 3.0.1 JSON
- ✅ **Checksum verification** — mikebom binary integrity verified via SHA256
- 📤 **Artifact upload** — automatically upload SBOM as workflow artifact
- 🔒 **Security-first** — pinned dependencies, minimal permissions, OpenSSF Scorecard

## Quick Start

```yaml
name: Generate SBOM
on: [push]

permissions:
  contents: read

jobs:
  sbom:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Generate SBOM
        uses: mfahlandt/mikebom-action@v0
        with:
          path: '.'
```

## Usage Examples

### Scan a source directory

```yaml
- uses: mfahlandt/mikebom-action@v0
  with:
    path: '.'
    format: 'cyclonedx-json'
    output-file: 'sbom.cdx.json'
```

### Scan a container image

```yaml
- uses: mfahlandt/mikebom-action@v0
  with:
    image: 'alpine:3.19'
    format: 'cyclonedx-json'
    output-file: 'image-sbom.json'
```

### Generate SPDX output

```yaml
- uses: mfahlandt/mikebom-action@v0
  with:
    path: '.'
    format: 'spdx-2.3-json'
    output-file: 'sbom.spdx.json'
```

### Include dev dependencies

```yaml
- uses: mfahlandt/mikebom-action@v0
  with:
    path: '.'
    include-dev: 'true'
```

### Offline mode (air-gapped)

```yaml
- uses: mfahlandt/mikebom-action@v0
  with:
    path: '.'
    offline: 'true'
```

### Pin a specific mikebom version

```yaml
- uses: mfahlandt/mikebom-action@v0
  with:
    path: '.'
    mikebom-version: 'v0.1.0-alpha.14'
```

## Inputs

| Input | Description | Default |
|-------|-------------|---------|
| `path` | Directory to scan (mutually exclusive with `image`) | `.` (if `image` not set) |
| `image` | Container image reference or tarball (mutually exclusive with `path`) | |
| `format` | Output format: `cyclonedx-json`, `spdx-2.3-json`, `spdx-3.0.1-json` | `cyclonedx-json` |
| `output-file` | Output file path for the SBOM | `sbom.json` |
| `upload-artifact` | Upload SBOM as workflow artifact | `true` |
| `artifact-name` | Name of the uploaded artifact | `sbom` |
| `mikebom-version` | mikebom release version to use | `v0.1.0-alpha.14` |
| `include-dev` | Include dev/test/optional dependencies | `false` |
| `offline` | Disable outbound network calls for enrichment | `false` |
| `image-src` | Image source order: `docker`, `remote`, or `docker,remote` | `docker,remote` |

## Outputs

| Output | Description |
|--------|-------------|
| `sbom-path` | Absolute path to the generated SBOM file |

## Supported Platforms

| Runner OS | Architecture | Status |
|-----------|-------------|--------|
| `ubuntu-latest` | x86_64 | ✅ Supported |
| `ubuntu-latest` | aarch64 | ✅ Supported |
| `macos-latest` | aarch64 (Apple Silicon) | ✅ Supported |

## Security

This action follows security best practices:

- All third-party actions are **pinned by full SHA commit hash**
- The mikebom binary is **verified against SHA256 checksums** published with each release
- The action requests **minimal permissions** (`contents: read`)
- **Dependabot** keeps dependencies up to date automatically
- **OpenSSF Scorecard** monitors the project's security posture weekly

See [SECURITY.md](SECURITY.md) for vulnerability reporting instructions.

## How It Works

1. Detects the runner's OS and architecture
2. Downloads the matching mikebom binary from the [kusari-sandbox/mikebom releases](https://github.com/kusari-sandbox/mikebom/releases)
3. Verifies the binary's SHA256 checksum
4. Runs `mikebom sbom scan` with the specified inputs
5. Optionally uploads the generated SBOM as a workflow artifact

## About mikebom

[mikebom](https://github.com/kusari-sandbox/mikebom) generates SBOMs with:

- **SHA-256 content hashes** on every component
- **Real dependency graph edges** (not flat lists)
- **CycloneDX evidence blocks** with confidence scoring
- **Strict PURL encoding** across all ecosystems
- **Compiled binary identity** (ELF, Mach-O, PE)
- **Lockfile-aware** scanning (Cargo.lock, go.sum, package-lock.json, etc.)

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## License

This project is licensed under the Apache License 2.0 — see [LICENSE](LICENSE) for details.
