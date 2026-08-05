# UV

* Our preferred way of working with Python is to use a `uv` virtual environment.
* `uv` should be pre-installed and accessible to all users.

### Verify

```bash
uv --version
```

### Start

#### Existing project

```bash
cd existing-project
uv venv
source .venv/bin/activate
uv sync
```

#### New project

```bash
uv init myproject
cd myproject
```

### Use normally

* `uv add pandas`
* `uv sync`
* `uv run main.py`
