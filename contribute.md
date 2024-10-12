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

1. Navigate to the [Actions tab](https://github.com/2Toad/actions/actions)
2. Select the "Deploy to Prod" workflow
3. Click "Run workflow".
4. Enter a version number using semantic versioning (e.g., `1.1.0`).
5. Click "Run workflow" to start the process.

This automated workflow will:
- Create a new release with the specified version number
- Generate release notes
- Update the corresponding major version tag (e.g. `v1` will point to v1.x)
