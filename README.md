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
        uses: actions/checkout@v4

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
- `include_dev_dependencies` (optional): A boolean value to determine whether development dependencies should be included in the scan. Default is "true".

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
        uses: actions/checkout@v4

      - name: Install Trivy
        uses: 2Toad/actions/install-trivy@v1

      - name: Run Trivy SCA Scan
        uses: 2Toad/actions/run-trivy@v1
        with:
          severity: "HIGH,CRITICAL"
          skip_dirs: "dist"
          skip_files: "Dockerfile"
          include_dev_dependencies: "false"
```

## Contributing 🤝

So you want to contribute to the 2Toad Actions project? Fantastic! Please read the [Contribute](./contribute.md) doc to get started.