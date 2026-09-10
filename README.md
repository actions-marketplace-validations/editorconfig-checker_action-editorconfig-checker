# Setup EditorConfig Action

This action uses [editorconfig-checker][usage] to validate files.

[usage]: https://github.com/editorconfig-checker/editorconfig-checker#usage

## Usage

### Pre-requisites

Create a workflow `.yml` file in your repositories `.github/workflows` directory.
An [example workflow](#example-workflow) is available below.
For more information, reference the GitHub Help Documentation for [Creating a workflow file][creating-a-workflow-file].

[creating-a-workflow-file]: https://help.github.com/en/articles/configuring-a-workflow#creating-a-workflow-file

### Inputs

| Field          | Description                                                                    |
| -------------- | ------------------------------------------------------------------------------ |
| `version`      | editorconfig-checker version to install (default: `v4.0.1`)                    |
| `github-token` | Token used to look up the release to download (default: `${{ github.token }}`) |

The `version` default is a pinned tag rather than `latest`, so that pinning this
action to a commit SHA also pins the editorconfig-checker binary it installs.
Set `version: latest` to opt back into always installing the newest release,
at the cost of the installed binary no longer being determined by your pin.

### Example workflow

```yaml
name: EditorConfig Checker

on:
  pull_request:
    branches:
      - main

jobs:
  editorconfig:
    runs-on: ubuntu-24.04
    steps:
      - name: Check out code
        uses: actions/checkout@v6

      - name: Set up editorconfig-checker
        uses: editorconfig-checker/action-editorconfig-checker@main

      - name: Run editorconfig-checker
        run: editorconfig-checker
```

## License

[MIT LICENSE](LICENSE)
