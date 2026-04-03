# 2Toad Actions 🚀

![GitHub Release](https://img.shields.io/github/v/release/2Toad/actions)

A collection of GitHub Actions.

## SCA
Software Composition Analysis

### install-trivy

This [GitHub Action](./install-trivy/action.yml) installs the Trivy SCA tool on the runner environment.

[Trivy](https://github.com/aquasecurity/trivy) is a comprehensive, open-source, vulnerability scanner used to detect security issues in container images, file systems, and software dependencies.

**Usage Example:**

```yaml
jobs:
  sca:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v6

      - name: Install Trivy
        uses: 2Toad/actions/install-trivy@v1
```

### run-trivy

This [GitHub Action](./run-trivy/action.yml) runs a Trivy SCA scan on the specified path in the repository. It uses Trivy to scan for vulnerabilities, misconfigurations, secrets, and license issues in the codebase. This action is designed to be flexible, allowing for the inclusion or exclusion of development dependencies and specific directories or files from the scan.

**Inputs:**

- `path` (required): The path to scan. Default is `.`
- `severity` (required): The severity levels to report. Defaults to all possible values `UNKNOWN,LOW,MEDIUM,HIGH,CRITICAL`.
- `skip_dirs` (optional): A comma-separated list of directories not to scan.
- `skip_files` (optional): A comma-separated list of files not to scan.
- `include_dev_dependencies` (optional): When `true` development dependencies are included in the scan. Default is "true".
- `fail_on_db_error` (optional): When `true` the action will fail if Trivy cannot download the vulnerability DB (and perform the vulnerability scan). Default is "true".
- `cache_db` (optional): When `true`, the Trivy vulnerability database is cached between workflow runs using GitHub Actions cache. If a database fetch fails due to rate limits or connectivity issues, the workflow automatically falls back to the cached database, preventing workflow failures. Default is "true".
- `ignored_licenses` (optional): A comma-separated list of licenses to ignore (e.g., `MPL-2.0,LGPL-2.1`).

**Caching and Fallback:**

When `cache_db` is enabled (the default), the action uses [GitHub Actions cache](https://github.com/actions/cache) to store the Trivy cache directory (`~/.cache/trivy`), which includes the vulnerability DB and Java DB. This provides:

1. **Automatic caching** — After a successful database download, the DB is cached and available for future workflow runs.
2. **Fallback on failure** — If Trivy fails to download the vulnerability DB (e.g., due to rate limits or network issues), the action automatically retries the scan using the cached database with `--skip-db-update`. This prevents workflow disruptions while still performing the security scan.
3. **Graceful degradation** — If no cached database exists and the download fails, behavior is controlled by `fail_on_db_error`: the action either fails (default) or continues with a warning.

> **Note:** The cached database may not contain the very latest vulnerability data. The action always attempts a fresh download first, only falling back to the cache when the download fails.

**Requirements:**

- Trivy must be installed (e.g., using the [2Toad/actions/install-trivy](#install-trivy) action)
- Code must be checked out (e.g., using the [actions/checkout](https://github.com/actions/checkout) action)
- For license scanning to work, the `node_modules` folder must be present

**Usage Example:**

```yaml
jobs:
  sca:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v6

      - name: Install Trivy
        uses: 2Toad/actions/install-trivy@v1

      - name: Run Trivy SCA Scan
        uses: 2Toad/actions/run-trivy@v1
        with:
          severity: "HIGH,CRITICAL"
          skip_dirs: "dist"
          skip_files: "Dockerfile"
          include_dev_dependencies: "false"
          ignored_licenses: "MPL-2.0"
```

## Contributing 🤝

So you want to contribute to the 2Toad Actions project? Fantastic! Please read the [Contribute](./contribute.md) doc to get started.