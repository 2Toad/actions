# Contribute to the 2Toad Actions project 🤝

Thank you for wanting to contribute to this project. With your help we can ensure these Actions remains a valuable contribution to the GitHub community.

## Steps for success

1. [Issues](https://github.com/2Toad/actions/issues):
   1. Always work off of an Issue. Please do not submit a Pull Request that is not associated with an Issue (create the Issue if necessary).
   2. If you are beginning work on an Issue, please leave a comment on the issue letting us know, and we'll assign the Issue to you. This way somebody else won't start working on the same Issue.
2. [Branches](https://github.com/2Toad/actions/branches):
   1. Always branch off of `main`, which contains the latest version of actions
3. [Pull Request](https://github.com/2Toad/actions/pulls) (PR):
   1. Make sure your PR is targeting the correct branch (see Step 2.i)
   2. At the top of your PR description write: "Fixes #_n_". Where _n_ is the number of the Issue your PR is fixing (e.g., `Fixes #33`). This will tell GitHub to associate your PR with the Issue.

## Deployment

### 1. Publish New Release

1. Navigate to [actions's releases](https://github.com/2Toad/actions/releases).
2. Click "Draft a new release":
   - **Choose a tag**: enter version (e.g., `v1.1.0`) and click "Create new tag"
   - **Target**: `main`
   - **Previous tag**: `auto`
   - **Release title**: (e.g., `1.1.0`)
   - **Description**: click the "Generate release notes"
   - [x] **Set as the latest release**
3. Click "Publish release".

2. ### Update Major Version Tag

After publishing a new release, update the major version tag using the following CLI commands:

1. Ensure you're on the main branch and have the latest changes:
   ```bash
   git checkout main
   git pull origin main
   ```
2. Update the major version tag:
   ```bash
   git tag -fa v1 -m "Update v1 tag to latest release" v1.1.0
   git push origin v1 --force
   ```
   Replace `v1` with the appropriate major version (e.g., v2) and `v1.1.0` with the newest release (e.g., v2.0.3).
