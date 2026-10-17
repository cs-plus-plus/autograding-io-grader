# CS++ Autograding IO Grader

A maintained, drop-in continuation of [`classroom-resources/autograding-io-grader@v1`](https://github.com/classroom-resources/autograding-io-grader).
GitHub retired GitHub Classroom on 2026-08-28 and archived its autograding actions on 2026-09-04.
This repository keeps them working for teachers who grade in GitHub Actions, with or without
[CS++](https://csplusplus.com/github).

**To switch, change one line per step:**

```yaml
# before
uses: classroom-resources/autograding-io-grader@v1
# after
uses: cs-plus-plus/autograding-io-grader@v1
```

Inputs, outputs and results are identical to `classroom-resources/autograding-io-grader@v1`. The code is the original v1 release; this
fork changes only the action runtime (now Node 24) and the action's name and author.
Issues and security reports: [open an issue](https://github.com/cs-plus-plus/autograding-io-grader/issues) or email
kevin@csplusplus.com.

Originally written by GitHub and released under the MIT License, which this fork keeps
(see `LICENSE.md`). It is not affiliated with or endorsed by GitHub.

---

## Original README (v1)

## GitHub Classroom IO Grader

### Overview
**GitHub Classroom IO Grader** is a plugin for GitHub Classroom's Autograder. Use it to ensure student executables output the correct values on tests.

### Key Features
- **Automatic Grading**: Test student code submissions and provide immediate feedback.
- **Customizable Test Setup**: Define pre-test setup commands and specific testing commands.
- **Flexible Output Comparison**: Supports multiple methods to compare the stdout output.
- **Timeout Control**: Limit the runtime of tests to prevent excessive resource usage.

### Inputs

| Input Name | Description | Required |
|------------|-------------|----------|
| `test-name` | The unique identifier for the test. | Yes |
| `setup-command` | Command to execute prior to the test, typically for environment setup or dependency installation.| No |
| `command` | The main command executed during the test. It receives input via stdin (if provided) and its output is evaluated against `expected-output` based on the `comparison-method`. | Yes |
| `input` | The input data that will be passed to the command via stdin. | No |
| `expected-output` | The expected output that the command should print to stdout. | Yes |
| `comparison-method` | Defines how the stdout output will be compared. Supported values are `included`, `exact`, and `regex`. | Yes |
| `timeout` | Duration (in minutes) before the test is terminated. Defaults to 10 minutes with a maximum limit of 6 hours.| No |
| `max-score` | The maximum amount of points a student can receive for this test.| No |


### Outputs

| Output Name | Description |
|-------------|-------------|
| `result` | Outputs the result of the grader, indicating the success or failure of the test. |

### Usage

1. Add the GitHub Classroom IO Grader action to your workflow.

```yaml
name: Autograding Tests

on:
  push

jobs:
  run-tests:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout code
      uses: actions/checkout@v4
    - name: Run Autograding Tests
      uses: education/autograding-io-grader@v1
      with:
        test-name: 'Test Name'
        command: './bin/shout'
        input: 'hello'
        expected-output: 'HELLO'
        comparison-method: 'exact'
    - name: Autograding Reporter
      uses: ...
