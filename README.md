# Pytest Runner

A github action to simply the running of pytest along with the publishing of results.

Essentially a configurable fast pytest runner (with sane options auto set) with additional use of [EnricoMi/publish-unit-test-result-action](https://github.com/EnricoMi/publish-unit-test-result-action) to publish the results.

## How to use

### Example 1: Basic setup, no arguments needed

This will run unit tests from your root workspace folder, finding tests throughout the codebase. It will publish results following the default setup of [EnricoMi/publish-unit-test-result-action](https://github.com/EnricoMi/publish-unit-test-result-action).

```yml
name: Running unit tests
uses: propertylift/github.action.pytest@latest
```

### Example 2: Customise use

In this example, we've opted not to publish the results. We're also saying our codebase is located in a subfolder and we're testing a specific folder.

```yml
name: Running unit tests
uses: propertylift/github.action.pytest@main
with:
  publish: false
  source: custom/path/to/code
  testFolder: tests # -> custom/path/to/code/tests
  githubToken: ${{ env.GITHUB_TOKEN }}
```

Use following example for publishing results in PR during it's testing or review

```yml
- name: Unit test with pytest
  uses: bricklanetech/github.action.pytest@main
  with:
    args: '--ruff'
    publish: true
    githubToken: ${{ env.GITHUB_TOKEN }}
    pythonVersion: ${{ env.PYTHON_VERSION }}
```


## Inputs

| Parameter Name | Description                                                                                       | Required | Default                    |
| -------------- | ------------------------------------------------------------------------------------------------- | -------- | -------------------------- |
| source         | The directory where the python source code is located                                             | No       | current directory          |
| configuration  | File path to the pytest configuration file (.ini).                                                | No       | -                          |
| testFolder     | The directory where the tests are located (from the source path), if targetting a specific folder | No       | -                          |
| args           | Additional arguments to pass to pytest.                                                           | No       | -                          |
| outputFile     | The file to write the test results to.                                                            | No       | `test-results/results.xml` |
| publish        | Whether to publish the test results.                                                              | No       | true                       |
| githubToken    | The GitHub token to use for checkouting and publishing the test results.                          | Yes      | -                          |
| pythonVersion  | The python version to use.                                                                        | No       | 3.9                        |
