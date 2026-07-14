# Python CI Lab Guide with GitHub Copilot

## Introduction

This lab walks you through creating a simple Python application and setting up a continuous integration pipeline using GitHub Actions and GitHub Copilot.

By the end of this lab, you will know how to:

- Create and clone a GitHub repository.
- Set up a Python virtual environment.
- Use GitHub Copilot to scaffold Python source code and tests.
- Create a GitHub Actions CI workflow.
- Run linting and tests automatically on GitHub.
- Use Copilot Chat to troubleshoot CI failures.

## Prerequisites

Before starting, make sure you have:

- A GitHub account with GitHub Copilot enabled.
- Visual Studio Code installed.
- The GitHub Copilot and GitHub Copilot Chat extensions installed in VS Code.
- Python 3.10 or later installed locally.
- Git installed locally.

## Step 1: Create a Repository and Scaffold the App

### 1. Create and Clone a Repository

Create a new GitHub repository. Example name:

```text
copilot-ci-python-lab
```

Clone the repository to your local machine and open it in VS Code.

### 2. Create a Python Virtual Environment

Open a new terminal in VS Code.

Run the following command:

```powershell
python -m venv .venv
```

Activate the virtual environment on Windows:

```powershell
.venv\Scripts\activate
```

If you are using Ubuntu or another Linux environment, use:

```bash
source .venv/bin/activate
```

Screenshot placeholder:

```text
[Insert screenshot showing the virtual environment activated in the VS Code terminal.]
```

### 3. Install Dependencies

After activating the virtual environment, install `pytest` and `flake8`:

```powershell
pip install pytest flake8
```

### 4. Scaffold the Python App with Copilot

In VS Code:

1. Open a new terminal.
2. Open GitHub Copilot Chat.
3. Enter the following prompt:

```text
Create a Python function add(a,b) in src/math_utils.py and a pytest test in tests/test_math_utils.py that asserts add(2,3) == 5.
```

4. Click **Run** or accept Copilot's suggested changes.

Copilot should create the following folders and files:

```text
src/
  math_utils.py

tests/
  test_math_utils.py
```

Screenshot placeholder:

```text
[Insert screenshot showing the src and tests folders created by Copilot.]
```

Example `src/math_utils.py`:

```python
def add(a, b):
    return a + b
```

Example `tests/test_math_utils.py`:

```python
from src.math_utils import add


def test_add():
    assert add(2, 3) == 5
```

Run the test locally:

```powershell
pytest
```

You should see the test pass.

## Step 2: Draft the CI Workflow with Copilot

Create this folder and file in your repository:

```text
.github/workflows/ci.yml
```

Open Copilot Chat and enter this prompt:

```text
Draft a GitHub Actions workflow for Python that runs on push and pull_request, installs dependencies, runs flake8 and pytest, and uses caching.
```

Copilot may generate a workflow similar to this:

```yaml
name: Python CI

on:
  push:
  pull_request:

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - name: Check out repository
        uses: actions/checkout@v4

      - name: Set up Python
        uses: actions/setup-python@v5
        with:
          python-version: "3.10"
          cache: "pip"

      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          pip install pytest flake8

      - name: Run flake8
        run: flake8 src tests

      - name: Run pytest
        run: pytest
```

Screenshot placeholder:

```text
[Insert screenshot showing the ci.yml file in VS Code.]
```

## Step 3: Commit, Push, and Observe the Workflow

Stage your files:

```powershell
git add .
```

Commit your changes:

```powershell
git commit -m "Add Python app and CI workflow"
```

Push your changes to GitHub:

```powershell
git push
```

After pushing, open your GitHub repository in a browser.

Check that:

1. The `src`, `tests`, and `.github/workflows` folders were uploaded.
2. The GitHub Actions workflow started automatically.
3. The workflow completed successfully.

Screenshot placeholders:

```text
[Insert screenshot showing uploaded folders and files in GitHub.]
[Insert screenshot showing a successful GitHub Actions workflow run.]
```

If the workflow fails, open the failed job logs and use Copilot Chat to help interpret the error.

## Step 4: Optional Enhancements

Try these enhancements to challenge your understanding.

### Add Coverage Reporting

Install coverage tooling:

```powershell
pip install pytest-cov
```

Update the workflow to run:

```powershell
pytest --cov=src
```

Example Copilot prompt:

```text
Update this GitHub Actions workflow to run pytest with coverage and upload the coverage report as an artifact.
```

### Add Matrix Builds

Ask Copilot:

```text
Update this workflow to test against Python 3.10, 3.11, and 3.12 using a matrix build.
```

### Add Security Scanning

Ask Copilot:

```text
Convert this workflow to include a Bandit security scan.
```

Or:

```text
Add CodeQL scanning to this Python GitHub Actions workflow.
```

## Copilot Prompt Ideas

Use these prompts to deepen your understanding:

```text
Explain each step in this YAML.
```

```text
Add caching for pip dependencies.
```

```text
Fail workflow if coverage is below 80%.
```

```text
Convert this workflow to include a Bandit security scan.
```

## Troubleshooting Tips

- Confirm that `src/math_utils.py` exists.
- Confirm that `tests/test_math_utils.py` exists.
- Check that your import path is correct.
- Make sure dependencies are installed in the GitHub Actions runner.
- Run `pytest` locally before pushing.
- Run `flake8 src tests` locally before pushing.
- Use Copilot Chat to interpret error logs and suggest fixes.

## Expected Final Repository Structure

Your repository should look similar to this:

```text
copilot-ci-python-lab/
  .github/
    workflows/
      ci.yml
  src/
    math_utils.py
  tests/
    test_math_utils.py
```

## Completion Checklist

- Created a GitHub repository.
- Cloned the repository locally.
- Created and activated a Python virtual environment.
- Installed `pytest` and `flake8`.
- Used Copilot to create source code and tests.
- Created `.github/workflows/ci.yml`.
- Committed and pushed changes.
- Verified that GitHub Actions completed successfully.
