[![PyPI Downloads](https://static.pepy.tech/badge/deardir)](https://pepy.tech/projects/deardir)
[![codecov](https://codecov.io/gh/deardir/deardir/branch/main/graph/badge.svg)](https://codecov.io/gh/deardir/deardir)

# deardir

**Validate and optionally create project directory structures from JSON or YAML schema files.**

pypi ref: https://pypi.org/project/deardir/

---

## ➡️ Features

- Validate file/folder structures using declarative schema files
- Supports `.json`, `.yaml`, `.yml`, Python `dict` or `list` objects
- Optionally auto-creates missing directories and files
- Async live mode to continuously monitor a structure
- Python API and CLI interface

---

## ➡️ Installation

```bash
pip install deardir
```

Or if you are developing locally:

```bash
poetry install
```

---

## ➡️ Example Schema

### `schema.yml`

```yaml
- data
- src:
    - __init__.py
    - main.py
    - utils:
        - helpers.py
- README.md
- pyproject.toml
```

---

## ➡️ Usage

### Python

```python
from deardir import DearDir
from pathlib import Path

dd = DearDir(root_paths=[Path(".")], schema=Path("schema.yml"))
dd.create_missing = True
dd.validate()

print(dd.missing)   # Set of missing paths
print(dd.created)   # Set of paths that were created
```

### Async live mode

```python

dd = DearDir([Path(".")], "schema.yml")
dd.create_missing = True

dd.live(interval=10, duration=60, mode=1)

# Thread
dd.live(interval=10, duration=60, mode=2)

# Synchron
dd.live(interval=10, duration=60, mode=0)

```

---

### CLI

```bash
deardir
deardir --help
deardir check --help
deardir --version
deardir check ./Tests --schema schema.yaml 
deardir check ./Tests --schema schema.yaml --create
#ASYNC LIVE WATCHER:
deardir watch ./Tests --schema schema.yaml --create --interval 1 --duration 10
```

---

## ➡️ Future Ideas (help wanted!)

- Improved CLI and JSON/HTML/Markdown reporting with colorized output  
- Support for optional files/folders and conditional rules in schema  
- Custom user-defined validation hooks  
- Auto-fix mode (e.g. create from templates, autofill missing entries)  
- File system watch mode with live validation (`--watch`)  
- GUI or web interface for drag-and-drop validation  
- GitHub Action / CI/CD integration  
- Multi-language support (English, German, ...)

---

## 📄 License

MIT

## Tests
