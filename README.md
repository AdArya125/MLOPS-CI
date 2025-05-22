# MLOPS-CI

This project is to demonstrate an end to end implementation of Continuous Integration.

# 🧪 Streamlit Power Calculator with GitHub Actions CI

This is a simple Python project that demonstrates how to:

- Build a **Streamlit** app that calculates the **square**, **cube**, and **fifth power** of a number.
- Write and run **unit tests** using `pytest`.
- Set up **Continuous Integration (CI)** with **GitHub Actions**.

## Features

- **Streamlit App**: Input a number and view its square, cube, and power of five instantly.
- **Unit Tests**: Ensures the correctness of the mathematical functions.
- **GitHub Actions CI**: Automatically runs tests on every push and pull request to the `main` branch.

## 📁 Project Structure

```
.
├── app.py               # Streamlit app
├── _test.py             # Pytest unit tests
├── .github/
│   └── workflows/
│       └── ci.yaml      # GitHub Actions workflow
└── README.md            # Project documentation
```

## Functions

```python
def square(n):
    return n ** 2

def cube(n):
    return n ** 3

def fifth_power(n):
    return n ** 5
```

## Tests (`_test.py`)

```python
import pytest

def test_square():
    assert square(2) == 4
    assert square(3) == 9

def test_cube():
    assert cube(2) == 8
    assert cube(3) == 27

def test_fifth_power():
    assert fifth_power(2) == 32
    assert fifth_power(3) == 243

def test_invalid_input():
    with pytest.raises(TypeError):
        square("string")
```

## CI/CD with GitHub Actions

The CI is configured via `.github/workflows/ci.yaml` to:

- Trigger on pushes and pull requests to `main`.
- Set up Python 3.11.
- Install dependencies (`pytest`, `streamlit`).
- Run the test suite.

### `ci.yaml` Workflow

```yaml
name: CI Workflow

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Set up Python
        uses: actions/setup-python@v2
        with:
          python-version: "3.11"

      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          pip install pytest streamlit

      - name: Run tests
        run: |
          pytest _test.py
```

## Running Locally

1. **Install dependencies**:

```bash
pip install streamlit pytest
```

2. **Run the app**:

```bash
streamlit run app.py
```

3. **Run the tests**:

```bash
pytest _test.py
```

## License

MIT License
