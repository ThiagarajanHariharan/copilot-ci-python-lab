# Python CI Lab with GitHub Copilot

Simple Python project for practicing GitHub Actions CI with `pytest` and `flake8`.

## Local Setup

```powershell
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
```

## Run Checks

```powershell
flake8 src tests
pytest
```
