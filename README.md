# Reusable workflows

### Run python tests

[`uses: tlambert03/workflows/.github/workflows/test_pyrepo.yml@main`](.github/workflows/test_pyrepo.yml)

Standard workflow to setup python and test a python package.

```yaml
    uses: tlambert03/workflows/.github/workflows/test_pyrepo.yml@main
    with:
      # The platform to run the tests on
      platform: 'ubuntu-latest'
      # The python version to use
      python-version: '3.x'
      # Whether tests require a Qt environment & xvfb on linux
      use-qt: false
      # Whether to use tox to run tests (otherwise pytest)
      use-tox: false
      # Comma-separated extras to install for testing
      testing-extras: 'test'
      # Additional arguments to pass to pytest (if use-tox is false)
      pytest-args: '-v --color --cov --cov-report=xml --cov-report=term-missing'
      # Whether to cancel in-progress workflows
      cancel-in-progress: true
```

<details>

<summary>Example usage</summary>

```yaml
name: CI

jobs:
  run_tests:
    name: ${{ matrix.platform }} (${{ matrix.python-version }})
    strategy:
      fail-fast: false
      matrix:
        python-version: ["3.9", "3.10", "3.11"]
        platform: [ubuntu-latest, macos-latest, windows-latest]
    uses: tlambert03/workflows/.github/workflows/test_pyrepo.yml@main
    with:
      platform: ${{ matrix.platform }}
      python-version: ${{ matrix.python-version }}
      use-tox: true
      use-qt: true
```

</details>

### Check Manifest

[`uses: tlambert03/workflows/.github/workflows/check_manifest.yml@main`](.github/workflows/check_manifest.yml)

Workflow to validate that all files in the repo are included in the manifest.

```yaml
    uses: tlambert03/workflows/.github/workflows/check_manifest.yml@main
    with:
      # The python version to use
      python-version: '3.x'
```

<details>

<summary>Example usage</summary>

```yaml
name: CI

jobs:
  check_manifest:
    uses: tlambert03/workflows/.github/workflows/check_manifest.yml@main
```

</details>

### Deploy to PyPI

[`uses: tlambert03/workflows/.github/workflows/deploy_pypi.yml@main`](.github/workflows/deploy_pypi.yml)

Workflow to validate that all files in the repo are included in the manifest.

```yaml
    uses: tlambert03/workflows/.github/workflows/deploy_pypi.yml@main
    with:
      # The TWINE token (API Key) to use for deployment 
      twine_api_key: <REQUIRED>
      # The platform to build on
      platform: 'ubuntu-latest'
      # The python version to use
      python-version: '3.x'
      # Whether to autogenerate github release notes
      generate_release_notes: true
```

<details>

<summary>Example usage</summary>

```yaml
name: CI

jobs:
  deploy:
    uses: tlambert03/workflows/.github/workflows/deploy_pypi.yml@main
    with:
       twine_api_key: ${{ secrets.TWINE_API_KEY }}
```

</details>