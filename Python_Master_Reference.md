# 🐍 The Complete Python Master Reference

**CLI commands & subcommands · the whole language · standard library · full step-by-step tutorials**

> **The Python edition of the Command-Line Master Reference.** Covers every way you *run* Python (interpreter flags, `pip`, `venv`, packaging tools, debuggers), the complete core language with every important method table, the essential standard library, 10 hands-on tutorials, and 8 quick-reference appendices. Examples target **Python 3.10–3.13**.
>
> Conventions: `command` = type exactly · `⟨required⟩` · `[optional]` · `a|b` = choose one · ⚠ = destructive/risky · † = deprecated or removed (modern replacement given) · `$` = shell prompt (CMD/PowerShell/Bash all fine) · `>>>` = Python REPL.

---

## Table of Contents

**PART 0 — Getting Started (Beginner Course)**
0.1 Python versions & implementations · 0.2 Installing Python everywhere · 0.3 Running Python: 7 ways · 0.4 The REPL & IPython · 0.5 Virtual environments & the packaging zoo · 0.6 Getting help anywhere · 0.7 Your first 10 programs

**PART 1 — The Python Command Line: every tool & subcommand**
1. `python` — every interpreter flag & env var · 2. `py` launcher (Windows) · 3. `pip` — every subcommand & key flags · 4. Environments: `venv` · `virtualenv` · `pipx` · `poetry` · `pipenv` · `conda` · `uv` · 5. `python -m` toolbox (pydoc, http.server, json.tool, timeit, cProfile, pdb, compileall, zipfile…)

6. Packaging & publishing (`pyproject.toml`, `build`, `twine`, setuptools) · 7. Testing (`pytest` all flags, `unittest` CLI, `coverage`) · 8. Quality tools (`ruff`, `black`, `isort`, `mypy`, `flake8`, `pylint`, `bandit`, `pre-commit`) · 9. Debugging & profiling (`pdb` — every command, `cProfile`, `timeit`, `tracemalloc`) · 10. Jupyter & notebooks

**PART 2 — The Language: complete syntax reference**
11. Structure & syntax rules · 12. Built-in types — every method (`str`, `list`, `dict`, `set`, `bytes`…) · 13. Operators & precedence — full tables · 14. Strings deep-dive: slicing, all methods, f-string format specs, `re` regex

15. Control flow: `if`/`match`/`for`/`while`, comprehensions, generators, `itertools` — every function · 16. Functions: `*args`/`**kwargs`, lambdas, closures, decorators, `functools`, typing · 17. Classes & OOP: inheritance, `dataclasses`, properties, dunder protocol · 18. Exceptions: full hierarchy + best practices · 19. Modules, packages & imports

20. Files & I/O: `open`, `pathlib` (all methods), `os`/`shutil`, JSON/CSV/pickle, `sqlite3`, `tempfile` · 21. Concurrency: `threading`, `multiprocessing`, `asyncio`, `concurrent.futures` · 22. Standard-library essentials: `datetime`, `collections`, `itertools`, `random`, `hashlib`, `subprocess`, `argparse` (full tutorial), `logging` (full tutorial), networking, `zipfile`

**PART 3 — Hands-On Tutorials (T1–T10)**
T1 Your first hour · T2 Parse a log file → CSV report · T3 Consume any REST API (JSON) · T4 Build a real CLI app with `argparse` · T5 OOP with dataclasses: an inventory manager · T6 Package & publish a library to PyPI · T7 Test like a pro with `pytest` · T8 Automate the boring stuff (files, Excel, email) · T9 Async: concurrent downloader · T10 Debug & profile like a detective

**PART 4 — Appendices**
A. A–Z command/tool index · B. All built-in functions (70) · C. Dunder methods protocol table · D. f-string & `format()` spec table · E. Exceptions hierarchy tree · F. One-liner cookbook · G. Traceback decoding, common errors, best-practice checklist · H. Every Python library — complete stdlib + essential third-party

---
---

# PART 0 — GETTING STARTED (Beginner Course)

## 0.1 Python versions & implementations

| Thing | What to know |
|---|---|
| **Python 3.x** | The present & future. Use 3.11+ (25–60 % faster than 3.10); 3.13 is current stable |
| **Python 2.7** † | Dead since 2020-01-01. If you meet legacy code, port it (`2to3`) |
| **CPython** | The reference implementation you download from python.org — what “Python” means by default |
| **PyPy** | JIT-compiled, often 4–10× faster for long-running pure-Python code; lags CPython by a version or two |
| **MicroPython / CircuitPython** | Python for microcontrollers (ESP32, Raspberry Pi Pico) |
| **IronPython / Jython** † | .NET / JVM ports — niche today |

Version check — do this first, always: `$ python --version` (or `py -V` on Windows). The interpreter reports e.g. `Python 3.12.4`. Any 3.10+ is fine for this entire document.

## 0.2 Installing Python everywhere

| Platform | Method |
|---|---|
| Windows | `winget install Python.Python.3.13` (or from [python.org](https://python.org) — **tick “Add python.exe to PATH”** in the installer) |
| Windows (multi-version) | Install several side by side; the `py` launcher picks: `py -3.12`, `py -0` lists all |
| macOS | `brew install python@3.13` (macOS also ships a system python3 — check `python3 -V`) |
| Ubuntu/Debian | `sudo apt install python3 python3-pip python3-venv python3-full` |
| Fedora/RHEL | `sudo dnf install python3 python3-pip` |
| From source | `./configure && make -j && sudo make altinstall` (use `altinstall` so you don’t shadow the system python) |

**Rule #1:** never install project packages into the system Python — use a virtual environment (0.5). On Windows, also grab [VS Code](https://code.visualstudio.com) + the Python extension; on any platform an editor with a language server (VS Code, PyCharm, Neovim+pyright) transforms the experience.

## 0.3 Running Python: 7 ways

| # | How | Example |
|---|---|---|
| 1 | REPL | `$ python` → `>>>` prompt (exit: `exit()` or Ctrl+D / Ctrl+Z⏎) |
| 2 | Script file | `$ python hello.py` |
| 3 | One-liner | `$ python -c "print(2**38)"` |
| 4 | Module | `$ python -m http.server 8000` |
| 5 | Stdin pipe | `$ echo "print('hi')" \| python` or `python < script.py` |
| 6 | Interactive-after-run | `$ python -i script.py` — drops into REPL **with** the script’s variables (great for poking at results) |
| 7 | Executable script | Add shebang `#!/usr/bin/env python3`, `chmod +x`, run `./script.py` (Unix); on Windows use `py script.py` or `.py` file association |

Bonus: `$ python -m pydoc -b` opens browsable docs of every installed module; `python -m this` prints the Zen of Python.

## 0.4 The REPL & IPython

| REPL trick | What it does |
|---|---|
| `_` | Last result value |
| `_3` (IPython) | Result number 3 |
| `Tab` | Completion (names, paths, methods) |
| `history` (IPython) | Show session history |
| `help(x)` | Docs on object x |
| `dir(x)` | Everything x has |
| `x?` / `x??` (IPython) | Quick help / full source |
| `%timeit expr` (IPython) | Micro-benchmark |
| `%run script.py` (IPython) | Run file in session |
| `%pip install x` (IPython/Jupyter) | Pip inside the right environment |
| `python -q` | Start REPL without banner |
| `PYTHONSTARTUP=file` env | Auto-run on every REPL start |

Upgrade once comfortable: `$ pip install ipython` → run `ipython`. Colored output, magic commands (`%`), `?` help, shell escape (`!ls`), and syntax-highlighted input.

## 0.5 Virtual environments & the packaging zoo

**The problem:** project A needs `requests==2.31`, project B needs `2.32`. Install both into one global Python → pain. **The fix:** per-project isolated environments.

```bash
python -m venv .venv            # 1. create (one-time per project)
source .venv/bin/activate       # 2. activate (Linux/macOS)
.venv\Scripts\activate          #    (Windows CMD/PowerShell)
python -m pip install -U pip    # 3. fresh envs ship an old pip — upgrade
pip install requests            # 4. install into the env only
deactivate                      # 5. leave the env
```

An env is just a folder (here `.venv/`) containing a copy/symlink of the interpreter plus its own `site-packages`. Delete the folder = delete the env. Commit a `requirements.txt` (`pip freeze > requirements.txt`), never the `.venv/` folder itself.

| Tool | What it is | When to use |
|---|---|---|
| `venv` | Built-in env creator | Default choice, zero install |
| `virtualenv` | Third-party, faster, more features | Fine, but `venv` usually enough |
| `pip` | Package installer from PyPI | Inside every env |
| `pipx` | Installs CLI **apps** into their own envs (`pipx install black`) | For tools, not libraries |
| `poetry` | Env + dependency + build + publish, all-in-one (`pyproject.toml`) | Modern library/app workflow |
| `pipenv` | Pip + venv glue with Pipfile | Declined in popularity |
| `conda` / `mamba` | Env manager for Python **and** C/Fortran stacks (science) | Data science, numpy/CUDA needs |
| `uv` ⭐ | Rust-based, 10–100× faster pip/venv/poetry replacement | The 2024+ modern default for speed |

## 0.6 Getting help anywhere

| Where | Command |
|---|---|
| REPL | `help(len)`, `help("re")`, `dir(str)` |
| Shell docs | `python -m pydoc re.findall`, `pydoc -b` (browser), `pydoc -w module` (writes .html) |
| Signatures live | `import inspect; inspect.signature(func)` |
| Official docs | [docs.python.org/3](https://docs.python.org/3/) — tutorial, library reference, HOWTOs |
| Error → answer | Paste the **last line** of a traceback into a search; add “python3” |
| PEPs | Index of Python Enhancement Proposals — the design documents (`peps.python.org`) |

## 0.7 Your first 10 programs

```python
# 1 — print & arithmetic
print("Hello, Python!", 2 + 2, 10 / 4, 10 // 4, 10 % 4, 2 ** 10)

# 2 — variables need no declarations
name, age = "Matin", 30
print(f"{name} will be {age + 1} next year")     # f-string

# 3 — a list, a loop
for i in [3, 1, 4, 1, 5]:
    print(i * "*")

# 4 — conditions
temperature = 31
print("hot" if temperature > 28 else "fine")

# 5 — function
def greet(who="world"):
    return f"Hello, {who}!"
print(greet(), greet("Python"))

# 6 — dictionary
book = {"title": "Dune", "year": 1965}
book["author"] = "Frank Herbert"
print(book["title"].upper())

# 7 — input (note: always a string!)
age = int(input("Your age? "))
print("Days alive ≈", age * 365.25)

# 8 — file write & read
with open("notes.txt", "w", encoding="utf-8") as f:
    f.write("line 1\nline 2\n")
print(open("notes.txt").read().splitlines())

# 9 — comprehension
squares = [n * n for n in range(1, 11) if n % 2 == 1]
print(squares)

# 10 — import & use the battery included
from datetime import date
from pathlib import Path
print(date.today(), "· cwd:", Path.cwd().name)
```

---
---

# PART 1 — THE PYTHON COMMAND LINE: EVERY TOOL & SUBCOMMAND

## 1. `python` — Every Interpreter Flag

| Flag | Meaning |
|---|---|
| `python script.py arg1 arg2` | Run script; args land in `sys.argv[1:]` |
| `python -c "code"` | Run a one-liner (`python -c "import sys;print(sys.version)"`) |
| `python -m module [args]` | Run a library module as a program — the power user's secret (§5) |
| `python -` | Read the program from stdin |
| `python -i [script]` | Drop into the REPL after running (inspect live objects) |
| `python -q` | No banner in REPL |
| `python -V` / `--version` | Print version (add `-VV` for build+compiler detail) |
| `python -u` | Unbuffered stdout/stderr — **essential** for logs in Docker/pipes |
| `python -B` | Don't write `.pyc` bytecode caches |
| `python -B`-adjacent: `PYTHONPYCACHEPREFIX=dir` | Redirect all bytecode caches to one folder |
| `python -E` | Ignore all `PYTHON*` environment variables (clean runs) |
| `python -s` | Ignore user `site-packages` |
| `python -S` | Skip importing `site` at startup (minimal startup; you lose easy-install paths) |
| `python -I` | Isolated mode = `-E` + `-s` + safe `sys.path` (no script dir) |
| `python -O` / `-OO` | Optimizations: strip `assert` (`-O`), also docstrings (`-OO`) — sets `__debug__=False` |
| `python -P` (3.11+) | Don't prepend script's directory to `sys.path` (safer imports) |
| `python -b` / `-bb` | Warn / error on `bytes`↔`str` comparison traps |
| `python -v` | Verbose: trace every import (also `import verbose` style debugging) |
| `python -W action` | Warnings control: `default error ignore always module once` (`-W error::DeprecationWarning`) |
| `python -X dev` | Development mode: extra checks, debug allocator (also `-X utf8`, `-X frozen_modules=on`) |
| `python -X importtime` | Print per-module import timing — kills slow startup |
| `python --check-hash-based-pycs always` | Always validate cached bytecode |
| `python -m pdb script.py` | Start under the debugger (§9) |
| `python -m trace --trace script.py` | Line-by-line execution trace |

**Environment variables that matter**

| Variable | Effect |
|---|---|
| `PYTHONPATH=dir1:dir2` | Extra module search paths (try to avoid; use proper packaging) |
| `PYTHONHOME` | Relocate the stdlib — rarely needed, often harmful |
| `PYTHONSTARTUP=file` | Executed at every interactive startup |
| `PYTHONBREAKPOINT=0\|func` | Disable or retarget `breakpoint()` (e.g. `PYTHONBREAKPOINT=pudb.set_trace`) |
| `PYTHONWARNINGS=ignore` | Same as `-W` |
| `PYTHONDONTWRITEBYTECODE=1` | Same as `-B` |
| `PYTHONUNBUFFERED=1` | Same as `-u` (standard in Dockerfiles) |
| `PYTHONIOENCODING=utf-8` | Force stdio encoding (fix Windows accents) |
| `PYTHONHASHSEED=0` | Determinable hashing (reproducible dict order tests) |
| `PYTHONFAULTHANDLER=1` | Dump traceback on crashes (segfaults) |
| `VIRTUAL_ENV=path` | Set by venv activation — how your prompt knows |

## 2. `py` Launcher (Windows)

| Command | Meaning |
|---|---|
| `py` | Run newest installed Python 3 |
| `py -3.12 script.py` | Run with a specific version |
| `py -0` / `py --list` | List installed versions (`-0p` with paths) |
| `py -V:3.12` | Pin exact version (also works in shebangs: `#!/usr/bin/env python3.12` → `py` honors it) |
| `py -m venv .venv` | Create env with chosen interpreter |
| `py -3.13 -m pip list` | Pip of a specific version |
| `py -h` | Launcher help |

On Unix the equivalent is simply `python3.12` binaries on PATH, or `uv python pin 3.12`.

## 3. `pip` — Every Subcommand

> Run `pip --version` **inside your venv** to be sure you're installing into the right place. Universal flags on every subcommand: `-v/-vv/-vvv` verbosity, `-q` quiet, `--dry-run` (23.2+, install/list), `--no-color`, `--require-virtualenv` safety.

| Subcommand | Purpose · key flags |
|---|---|
| `pip install pkg` | Install latest from PyPI |
| `pip install pkg==1.4.2` | Exact pin · `pkg>=1.4,<2` ranges · `pkg!=1.5` exclusions |
| `pip install -r requirements.txt` | Install a pinned set |
| `pip install -e .` / `-e path` | **Editable** install (your local project, live-edited) |
| `pip install -U pkg` | Upgrade (`--upgrade`) |
| `pip install --pre pkg` | Allow pre-releases/betas |
| `pip install pkg -t dir` | Install into arbitrary target folder |
| `pip install -i URL pkg` | Alternate index (`--index-url`), `--extra-index-url URL` secondary |
| `pip install -f URL/pkg.whl` | Find links — direct wheel/house index |
| `pip install --no-deps pkg` | Skip dependency resolution |
| `pip install --only-binary=:all:` | Wheels only (no source builds) · `--no-binary pkg` |
| `pip install --require-hashes -r reqs` | Hash-pinned reproducible install |
| `pip install --report report.json pkg` | JSON manifest of what would be installed |
| `pip download pkg -d dir` | Fetch packages without installing |
| `pip uninstall pkg` | Remove (`-y` no-confirm; multiple names ok) |
| `pip list` | Installed packages — `--outdated`, `--uptodate`, `-e` (editables), `--format=freeze\|json\|columns` |
| `pip freeze` | Requirements-style output — `> requirements.txt` |
| `pip show pkg` | Version, location, deps, home page (`-f` = installed files) |
| `pip check` | Verify installed deps are mutually consistent (missing/conflicting) |
| `pip cache dir\|info\|list\|remove\|purge` | Manage the wheel cache |
| `pip config list\|get\|set\|edit\|unset` | Config file management (`--user`, `--global`, `--site` scopes) |
| `pip index versions pkg` | All versions available on the index |
| `pip hash file` | Compute hash for `--require-hashes` |
| `pip inspect` | Full environment report as JSON (3.11+ pip) |
| `pip wheel pkg` | Build wheels for packages |
| `pip debug` | Environment/pip diagnostics |
| `pip completion --bash\|zsh\|fish` | Shell autocompletion setup |
| `pip search` † | Removed (PyPI shut the endpoint) — use pypi.org search or `pip index` |
| `pip help [command]` | Built-in docs |

**The workflow that never breaks:** `python -m pip …` — guarantees pip belongs to *that* interpreter, however many Pythons you have.

## 4. Environment & Dependency Managers

### `venv` (built-in)

| Command | Meaning |
|---|---|
| `python -m venv .venv` | Create |
| `python -m venv .venv --system-site-packages` | Inherit global packages (rare) |
| `python -m venv .venv --upgrade-deps` | Create with fresh pip+setuptools |
| `python -m venv .venv --without-pip` | Bare env (then `ensurepip`) |
| `python -m ensurepip --upgrade` | Bootstrap pip into an env |

### `pipx` — CLI apps in isolated envs

| Command | Meaning |
|---|---|
| `pipx install black` | Install an app globally-but-isolated, `~/.local/bin/black` |
| `pipx install poetry --pip-args=...` | Install with pip args |
| `pipx list` | Installed apps |
| `pipx upgrade / upgrade-all` | Update |
| `pipx uninstall / uninstall-all` | Remove |
| `pipx inject app pkg` | Add a library into an app's env |
| `pipx run pkg@1.2 --args` | One-shot run without installing |
| `pipx ensurepath` | Fix PATH |

### `poetry`

| Command | Meaning |
|---|---|
| `poetry init` | Interactive `pyproject.toml` |
| `poetry new pkg` / `poetry install` | Scaffold project / install all deps |
| `poetry add requests` / `poetry add --group dev pytest` | Add dependency (respecting semver) |
| `poetry remove pkg` | Drop it |
| `poetry update` / `poetry lock` | Refresh deps / regenerate lock file |
| `poetry run pytest` | Run command inside env |
| `poetry shell` | Activate env shell |
| `poetry build` | sdist + wheel |
| `poetry publish` | To PyPI (`--build` both) |
| `poetry env info / use 3.12` | Env management |

### `conda` / `mamba`

| Command | Meaning |
|---|---|
| `conda create -n ml python=3.12 numpy` | New env with packages |
| `conda activate ml` / `conda deactivate` | Enter/leave |
| `conda install pkg` / `conda remove pkg` | Install/remove (conda-forge channel: `-c conda-forge`) |
| `conda env list` / `conda env export > env.yml` | List / export |
| `conda env create -f env.yml` | Recreate |
| `conda list` / `conda info` / `conda clean --all` | Inventory / info / cache purge |
| `conda update conda` | Self-update |

### `uv` — the fast modern toolchain

| Command | Meaning |
|---|---|
| `uv venv` / `uv venv -p 3.13` | Create env (blazing) |
| `uv pip install / list / freeze / uninstall …` | pip-compatible interface |
| `uv init project` / `uv add pkg` / `uv remove pkg` | Project management (pyproject+lock) |
| `uv sync` | Install exactly the lock file |
| `uv lock` / `uv upgrade` | Lock / upgrade deps |
| `uv run script.py` | Run inside the project env |
| `uv tool install ruff` / `uvx ruff check .` | pipx-style tools / ephemeral run |
| `uv python install 3.12` / `uv python list` | Manage interpreters themselves |
| `uv self update` | Update uv |

## 5. The `python -m` Toolbox

`python -m module` runs any module that has a `__main__`. The stdlib ships dozens of ready-made tools:

| Command | What it gives you |
|---|---|
| `python -m http.server 8000` | Instant web server for the current folder (add `--bind 127.0.0.1`, `--directory path`) |
| `python -m http.server 8000 --cgi` † | CGI mode (removed 3.13) |
| `python -m json.tool file.json` | Pretty-print / validate JSON (`--indent 2`, `-` stdin) |
| `python -m json.tool --json-lines f.ndjson` | Validate newline-delimited JSON |
| `python -m timeit "‘-’.join(map(str,range(50)))"` | Micro-benchmark a snippet |
| `python -m cProfile -s cumulative script.py` | Profile a whole program (§9) |
| `python -m pstats dump.prof` | Interactive profile browser |
| `python -m pdb script.py` | Run under the debugger |
| `python -m pydoc re.sub` / `pydoc -b` / `-p 1234` | Docs in terminal / browser / port |
| `python -m zipfile -l arch.zip` | List zip contents |
| `python -m zipfile -e arch.zip dir/` / `-c arch.zip files…` | Extract / create |
| `python -m tarfile -l/-e/-c …` | Same for tar archives |
| `python -m base64 file` | Encode/decode base64 from CLI |
| `python -m compileall src/` | Pre-compile bytecode (deployment/syntax check) |
| `python -m ensurepip --upgrade` | Bootstrap/repair pip |
| `python -m site` | Show module search paths |
| `python -m sysconfig` | Build/interpreter configuration |
| `python -m unittest discover` | Run test suite (§7) |
| `python -m venv .venv` | Environments (§4) |
| `python -m webbrowser -t "https://x"` | Open a URL in a browser |
| `python -m ast script.py` | Dump the parse tree |
| `python -m dis script.py` | Disassemble to bytecode |
| `python -m token` | Tokenizer dump |
| `python -m textwrap`? — no CLI | ✗ (library only; listed so you don't hunt) |
| `python -m this` | The Zen of Python 🎶 |
| `python -m antigravity` | 🪁 xkcd 352. You deserve a break |

## 6. Packaging & Publishing

**Anatomy of a `pyproject.toml`** (the modern standard — one file, no setup.py needed):

```toml
[build-system]
requires = ["setuptools>=69"]
build-backend = "setuptools.build_meta"

[project]
name = "coolpkg"                     # PyPI name
version = "1.0.0"                    # or dynamic from git tags
description = "Does cool things"
readme = "README.md"
requires-python = ">=3.10"
license = {text = "MIT"}
authors = [{name = "Matin", email = "you@example.com"}]
keywords = ["cli", "tools"]
classifiers = ["Programming Language :: Python :: 3", "License :: OSI Approved :: MIT License"]
dependencies = ["requests>=2.31", "rich>=13"]

[project.optional-dependencies]
dev = ["pytest", "ruff", "mypy"]

[project.scripts]
cool = "coolpkg.cli:main"            # creates the `cool` command on install

[project.urls]
Homepage = "https://github.com/xvviix/coolpkg"

[tool.setuptools.packages.find]
include = ["coolpkg*"]
```

| Tool | Commands |
|---|---|
| `pip install build` → `python -m build` | Produces `dist/*.whl` + `dist/*.tar.gz` |
| `pip install twine` → `twine check dist/*` | Validate metadata/readme rendering |
| `twine upload dist/*` | **Publish to PyPI** (token auth: `__token__` + API token) |
| `twine upload --repository testpypi dist/*` | Rehearse on TestPyPI first |
| `pip install dist/coolpkg-1.0.0-py3-none-any.whl` | Local install test |
| Legacy `setup.py` † | `python setup.py sdist bdist_wheel` — migrate to pyproject |

**Version bumping:** SemVer — MAJOR breaking / MINOR features / PATCH fixes. Dev releases: `1.1.0a1`, `1.1.0b2`, `1.1.0rc1`.

## 7. Testing

### `pytest` — the standard

| Invocation | Meaning |
|---|---|
| `pytest` | Run all tests in `test_*.py` / `*_test.py` |
| `pytest test_math.py` / `pytest test_math.py::test_add` | File / single test |
| `pytest -v` / `-vv` / `-q` | Verbose / extra-verbose / quiet |
| `pytest -x` | Stop on first failure (`--maxfail=3`) |
| `pytest -k "add and not slow"` | Select by keyword expression |
| `pytest -m slow` | Select by marker (`@pytest.mark.slow`) |
| `pytest -s` | Disable capture — see print() output |
| `pytest --lf` / `--ff` | Last-failed only / failed-first |
| `pytest --durations=10` | Slowest 10 tests |
| `pytest --tb=short\|long\|line\|no` | Traceback style |
| `pytest --cov=mypkg --cov-report=html` | Coverage (needs pytest-cov) → `htmlcov/` |
| `pytest -n auto` | Parallel (pytest-xdist) |
| `pytest --fixtures` / `--collect-only` | List fixtures / dry-run collection |
| `pytest --junitxml=report.xml` | CI output |
| `pip install pytest-mock` → `mocker.patch("mod.func")` | Mocking helper |

Core API (used in scripts): `assert`, `pytest.raises`, `pytest.fixture`, `pytest.mark.parametrize`, `pytest.approx`, `tmp_path`, `capsys`, `monkeypatch`.

### `unittest` CLI (stdlib)

| Command | Meaning |
|---|---|
| `python -m unittest` | Autodiscover (`discover -s tests -p "test_*.py"`) |
| `python -m unittest tests.test_math` | One module |
| `python -m unittest tests.test_math.TestAdd.test_ints` | One test |
| `-v` / `-q` | Verbosity |
| `-f` / `-c` / `-b` | Stop-first-fail / fast Ctrl+C / buffer output |
| `-k pattern` | Filter by name |
| `--locals` | Show locals in tracebacks |

### coverage

`pip install coverage` → `coverage run -m pytest` → `coverage report -m` (missing lines) → `coverage html`. Config in `.coveragerc` or pyproject `[tool.coverage.run]`.

## 8. Quality Tools — Lint, Format, Type-check

| Tool (install) | Command | Purpose |
|---|---|---|
| `ruff` ⭐ | `ruff check .` | Linter (100s of rules, flake8+isort+pyupgrade in one, Rust-fast) |
| | `ruff check --fix .` | Auto-repair |
| | `ruff format .` | Formatter (Black-compatible) |
| | `ruff rule RUF008` / `ruff linter` | Rule docs / list rules |
| `black` | `black .` | The formatter — `--check`, `--diff`, `--line-length 100` |
| `isort` | `isort .` | Sort imports (`--profile black`) |
| `mypy` | `mypy src/` | Static types — `--strict`, `--ignore-missing-imports` |
| `flake8` | `flake8 src/` | Classic linter (`--max-line-length 100`) |
| `pylint` | `pylint src/` | Deep style/score linter |
| `bandit` | `bandit -r src/` | Security scanner |
| `pre-commit` | `pre-commit run -a` | Run all hooks; `.pre-commit-config.yaml` glues the above into git |

**One modern combo to rule them all:** `uv tool install ruff` + `ruff check --fix . && ruff format .` + `mypy src` in CI. That replaces flake8+isort+black+pyupgrade at ludicrous speed.

## 9. Debugging & Profiling

### `pdb` — every command

Start: `python -m pdb script.py` · or drop in code: `import pdb; pdb.set_trace()` · or modern: `breakpoint()`.

| Pdb command | Action |
|---|---|
| `h` / `h cmd` | Help / help on command |
| `l [n]` / `ll` | List source (around line) / whole function |
| `w` / `where` | Stack trace, current frame marked |
| `u` / `d` | Up / down the stack frames |
| `b 42` / `b func` / `b file:line` | Set breakpoint |
| `b` | List breakpoints |
| `tbreak …` | Temporary breakpoint (dies after first hit) |
| `cl [n]` | Clear breakpoint(s) |
| `disable n` / `enable n` | Toggle without deleting |
| `condition n expr` | Conditional breakpoint |
| `ignore n count` | Skip next *count* hits |
| `commands n` | Auto-commands on hit (end with `end`; `silent` + print = logging) |
| `s` / `step` | Step **into** |
| `n` / `next` | Step **over** |
| `r` / `return` | Run until current function returns |
| `c` / `continue` | Run to next breakpoint |
| `unt [n]` | Run until line n (or next line > current) |
| `j n` / `jump` | Jump execution to line n (careful!) |
| `a` / `args` | Current function arguments |
| `p expr` / `pp expr` | Print / pretty-print |
| `whatis expr` | Type of expr |
| `source expr` / `display [expr]` | Show source of object / auto-print on each stop |
| `interact` | Full REPL at this point |
| `retval` / `exc` | Last return value / current exception |
| `alias name cmd` | Command macros |
| `exec stmt` | Execute statement in frame |
| `q` | Quit (hard exit) |

Better-looking alternatives: `pip install ipdb` (`import ipdb; ipdb.set_trace()`) or `pudb` (full-screen TUI), or just use your editor's debugger (VS Code: F5).

### `cProfile`

```bash
python -m cProfile -s cumulative script.py          # sorted by total time
python -m cProfile -o out.prof script.py            # save
python -m pstats out.prof                           # browse: sort cumulative / stats 10 / strip
```

Reading it: `ncalls` calls · `tottime` time in the function itself · `cumtime` including children · look for high `tottime` = your hotspot. GUI: `pip install snakeviz` → `snakeviz out.prof`.

### `timeit` / `tracemalloc`

```bash
python -m timeit "'-'.join(map(str, range(50)))"
python -m timeit -s "x=list(range(1000))" "x.sort()"
```

| Snippet | Use |
|---|---|
| `timeit.timeit(f, number=1_000)` | Library form |
| `python -X importtime -c "import requests" 2> imp.log` | Find slow imports |
| `tracemalloc.start()` … `tracemalloc.take_snapshot()` | Who allocates memory |
| `sys.settrace` / `sys.setprofile` | Build your own tracer |
| `faulthandler.enable()` (or `-X dev`) | Traceback on hard crashes |

## 10. Jupyter & Notebooks

| Command | Meaning |
|---|---|
| `pip install notebook jupyterlab` | Install |
| `jupyter lab` / `jupyter notebook` | Launch UI (browser tab) |
| `jupyter lab --no-browser --port=8889` | Headless/remote |
| `jupyter console` / `jupyter qtconsole` | Terminal / Qt console |
| `jupyter kernelspec list` | Installed kernels |
| `ipykernel` → `python -m ipykernel install --user --name venv --display-name "Py(venv)"` | Register a venv as kernel |
| `jupyter nbconvert --to script nb.ipynb` | Notebook → .py (`--to html/slides/pdf`) |
| `jupyter nbconvert --execute nb.ipynb --inplace` | Run all cells from CLI |
| `jupyter trust nb.ipynb` | Trust stored outputs |
| `jupyter --version` / `jupyter --data-dir` | Install info |

---
---

# PART 2 — THE LANGUAGE: COMPLETE SYNTAX REFERENCE

## 11. Structure & Syntax Rules

| Rule | Detail |
|---|---|
| Indentation | Blocks are defined by indentation (4 spaces by convention; never mix tabs/spaces) |
| Comments | `# to end of line`; docstrings: `"""…"""` first statement of module/class/function |
| Line continuation | `\` at EOL, or implicit inside `( )`, `[ ]`, `{ }` |
| Statements per line | `a = 1; b = 2` (semicolon) — discouraged |
| Names | Letters/digits/underscore, can't start with digit; `lower_snake` for functions/vars, `CapWords` for classes, `_private` convention, `__name__` dunders are reserved |
| Case | Everything is case-sensitive |
| Entry point | `if __name__ == "__main__": main()` — runs only when executed, not imported |
| Encoding | UTF-8 by default (declare only if you need something else) |
| Truthiness | False: `None, False, 0, 0.0, '', [], {}, set(), (), range(0)` — everything else truthy |
| Identity vs equality | `is` compares identity (same object), `==` compares value; use `is None`, never `== None` |

## 12. Built-in Types — Every Method

### Numeric

| Type | Notes / operations |
|---|---|
| `int` | Arbitrary precision! `7 // 2`=3 floor, `7 % 2`=1, `2 ** 64`, `int("ff", 16)`=255, `int("0b101", 0)`, `abs()`, `divmod(7,2)`→(3,1), `pow(b, e, mod)` fast modular |
| `float` | IEEE 754: `0.1 + 0.2 != 0.3` (use `math.isclose`, `decimal`, or `fractions`); `1e9`, `round(x, 2)` banker's rounding, `float("nan")`, `math.isnan` |
| `complex` | `3+4j`, `.real`, `.imag`, `abs()` = magnitude |
| `bool` | Subclass of int: `True + True` = 2 |
| `decimal.Decimal` | Exact decimal money math: `Decimal("0.10") + Decimal("0.20") == Decimal("0.30")` |
| `fractions.Fraction` | Exact rationals: `Fraction(1, 3) * 3 == 1` |

### `str` — all methods

| Method | Returns |
|---|---|
| `s.upper() lower() capitalize() title() swapcase() casefold()` | Case variants (`casefold` = aggressive, for matching) |
| `s.strip() lstrip() rstrip([chars])` | Trim edges (default whitespace) |
| `s.ljust(w) rjust(w) center(w[, fill])` | Pad to width |
| `s.zfill(w)` | Zero-pad (keeps sign) |
| `s.startswith(p) endswith(p)` | Prefix/suffix test (accept tuples) |
| `s.find(sub) rfind(sub)` | Index or −1 |
| `s.index(sub) rindex(sub)` | Index or `ValueError` |
| `s.count(sub)` | Occurrences |
| `s.replace(old, new[, count])` | Substitute |
| `s.split(sep) rsplit(sep) splitlines()` | Split (`None` = whitespace runs; `splitlines` respects \n \r\n) |
| `s.join(iterable)` | Glue: `",".join(words)` |
| `s.partition(sep) rpartition(sep)` | `(pre, sep, post)` 3-tuple |
| `s.removeprefix(p) removesuffix(p)` | Clean prefix/suffix removal (3.9+) |
| `s.strip`-family + `chars` arg | Trim specific chars |
| `s.encode("utf-8")` | → bytes (`errors="ignore\|replace\|strict"`) |
| `s.format(**kw)` / `s.format_map(m)` | `"{x:>10}".format(x=1)` |
| `s.maketrans(a,b)` + `s.translate(t)` | Character mapping |
| Tests: `isalnum() isalpha() isascii() isdecimal() isdigit() isnumeric() isidentifier() islower() isupper() isspace() istitle() isprintable()` | True/False |

### `list` & `tuple`

| Method | Returns |
|---|---|
| `l.append(x)` | Add at end |
| `l.extend(iter)` | Add many |
| `l.insert(i, x)` | Insert at position |
| `l.remove(x)` | Delete first ==x (`ValueError` if missing) |
| `l.pop([i])` | Remove & return (default last) |
| `l.clear()` | Empty it |
| `l.index(x[, start[, end]])` | Position or `ValueError` |
| `l.count(x)` | Occurrences |
| `l.sort(*, key=None, reverse=True)` | In-place sort |
| `l.reverse()` | In-place reverse |
| `l.copy()` | Shallow copy |
| `sorted(iter, key=, reverse=)` → new list · `reversed(iter)` → iterator | Non-mutating versions |
| `tuple` | Immutable — only `count` + `index`; `(1,)` single needs comma |
| `min/max/sum/any/all(iter)` | Aggregates |

### `dict`

| Method | Returns |
|---|---|
| `d[k]` | Get or `KeyError` |
| `d.get(k[, default])` | Get or default (None) |
| `d[k] = v` / `del d[k]` / `d.pop(k[, default])` / `d.popitem()` | Write / delete (KeyError) / delete+return / delete last inserted |
| `d.update(other)` | Merge in |
| `d.setdefault(k, default)` | Get-or-create |
| `d.keys() values() items()` | Views (live!) |
| `dict(**kw)`, `dict(zip(ks, vs))`, `d \| other` (3.9+), `d \|= other` | Construction / merge |
| `{k: v for k, v in pairs}` | Dict comprehension |
| `collections.OrderedDict`† / `defaultdict` / `Counter` | When plain dict isn't enough (§22) |

### `set` / `frozenset`

| Method | Returns |
|---|---|
| `s.add(x)` / `s.remove(x)` / `s.discard(x)` | Add / remove (KeyError) / remove (silent) |
| `s.pop()` / `s.clear()` | Arbitrary removal / empty |
| `s.update(*others)` | ` \|=` union in place |
| `s.union(o)` `s.intersection(o)` `s.difference(o)` `s.symmetric_difference(o)` | New set results — operators: `\| & - ^` |
| `s.issubset(o)` `s.issuperset(o)` `s.isdisjoint(o)` | Relations: `<=` `>=` |
| `{x for x in it if p}` | Set comprehension |
| `frozenset(iter)` | Immutable, hashable (usable as dict key) |

### `bytes` / `bytearray` / `memoryview`

| Method | Returns |
|---|---|
| `b"abc"` / `bytes(range(65,68))` / `"a".encode()` | Literal / from ints / from str |
| `b.decode("utf-8")` | → str |
| `b.hex()` / `bytes.fromhex("414243")` | Hex shuttle |
| `bytearray` | Mutable bytes — same methods as bytes + `append/extend/insert` |
| `memoryview(b)` | Zero-copy slice view (`mv[0]`, `mv.cast("I")`) |

### Other core types

| Type | Notes |
|---|---|
| `None` | The null singleton — test with `is None` |
| `range(start, stop, step)` | Lazy integer sequence — `range(10, 0, -2)` |
| `enumerate(it, start=0)` | `(index, item)` pairs |
| `zip(a, b, strict=False)` | Parallel iteration; `strict=True` errors on length mismatch (3.10+) |
| `slice(start, stop, step)` | `s[slice(1,None,2)]` == `s[1::2]` |
| `type(x)` / `isinstance(x, T)` / `issubclass(A, B)` | Type tools |

## 13. Operators & Precedence

| Category | Operators (high→low precedence order) |
|---|---|
| Grouping | `( )` |
| Call / index / attribute / slice | `f(x)` `x[i]` `x.attr` `x[a:b]` |
| Power | `**` |
| Unary | `+x -x ~x` |
| Multiply/divide | `* / // %` |
| Add/subtract | `+ -` |
| Shifts | `<< >>` |
| Bitwise AND | `&` |
| Bitwise XOR | `^` |
| Bitwise OR | `\|` |
| Comparisons / membership / identity | `< <= > >= == != in not in is is not` (chaining works: `1 < x < 10`) |
| not | `not x` |
| and | `a and b` |
| or | `a or b` |
| Conditional | `x if c else y` |
| Assignment | `= += -= *= /= //= %= **= &= \|= ^= <<= >>= :=`(walrus) |

**Walrus `:=`** assigns inside an expression: `while (chunk := f.read(8192)): …`. Floor `//` rounds toward −∞ on negatives: `-7 // 2 == -4`. `==` on `is`-looking things: small ints/strings may be interned — never rely on it.

## 14. Strings Deep-Dive

### Slicing — the complete rules

```python
s = "Pythonista"
s[0] s[-1]        # 'P', 'a'
s[2:5] s[:4] s[6:]     # 'tho', 'Pyth', 'ista'
s[::2] s[::-1]         # 'PtoiA' step-2; reversed copy
s[1:-1:3]              # start 1, stop before -1, step 3
```

Index out of range in `[i]` raises; slices never do (they clamp). Works identically on lists/tuples — learn once, use everywhere.

### f-strings & `format` — full spec mini-language

`f"{value:[[fill]align][sign][z][#][0][width][grouping][.precision][type]}"`

| Piece | Options |
|---|---|
| align | `<` left · `>` right · `^` center · `=` pad after sign |
| sign | `+` always · `-` only negatives · ` ` space for positives |
| `#` | Alternate form: `0x` prefix, keep trailing `.0` |
| `0` | Zero-pad (same as `fill=0, align==`) |
| width | Minimum width (can nest: `{v:{w}}`) |
| grouping | `_` or `,` thousands separators |
| precision | Digits after `.` |
| type | `d` int · `f` fixed · `e` sci · `g` general · `%` percent · `b o x X` int bases · `c` char · `s` string · `n` locale-aware |

```python
f"{3.14159:.2f}"          # '3.14'
f"{1234567:,}"            # '1,234,567'
f"{0.85:.1%}"             # '85.0%'
f"{255:#x} {255:b}"       # '0xff' '11111111'
f"{'hi':^10}"             # '    hi    '
f"{name=} / {x=}"         # 'name=...' debug prints the expression!
f"{dt:%Y-%m-%d}"          # datetime inline
f"{obj!r}"                # repr() instead of str()
```

### `re` — the regex module

| Function | Use |
|---|---|
| `re.search(p, s)` | First match anywhere → Match or None |
| `re.match(p, s)` | Anchored at start · `re.fullmatch` entire string |
| `re.findall(p, s)` | All matches (list; groups→tuples) |
| `re.finditer(p, s)` | Iterator of Match objects |
| `re.sub(p, repl, s, count=0)` | Replace (repl may be a function!) · `re.subn` also returns count |
| `re.split(p, s)` | Split by pattern |
| `re.compile(p)` | Precompiled pattern object — reuse it |
| `re.escape(s)` | Quote all metacharacters |
| Match `m` | `m.group(0/1/name)`, `m.groups()`, `m.groupdict()`, `m.start() end() span()`, `m[0]` |

Flags: `re.I` ignorecase · `re.M` ^$ per-line · `re.S` dot-matches-newline · `re.X` verbose · `re.A` ASCII. Pattern syntax: `\d \w \s \b` classes, `+ * ? {m,n}` reps, `[]` sets, `(...)` group, `(?:...)` non-capture, `(?P<name>…)`, lookarounds `(?=…) (?!…) (?<=…) (?<!…)`, alternation `|`.

## 15. Control Flow

### Conditionals

```python
if x > 100:        ...
elif x > 10:       ...
else:              ...

# ternary
label = "big" if x > 100 else "small"

# match (3.10+) — structural pattern matching
match command.split():
    case ["go", direction]:            print("moving", direction)
    case ["go", *rest]:                print("go many:", rest)
    case ["drop", item] if item != "": print("dropping", item)
    case ["quit" | "exit"]:            break
    case {"op": "add", "n": n}:        total += n        # mapping patterns
    case Point(x=0, y=y):              ...               # class patterns
    case _:                            print("unknown")
```

### Loops

```python
for item in iterable: ...          # the one loop
for i, item in enumerate(items, 1): ...
for a, b in zip(xs, ys): ...
while condition: ...
break                               # exit loop
continue                            # next iteration
else:                              # runs only if loop finished WITHOUT break — unique to Python
    print("no break happened")
for n in range(10, 0, -1): ...     # countdown
```

### Comprehensions — all four

```python
[n*n for n in range(10) if n % 2 == 0]           # list
{n: n*n for n in range(5)}                       # dict
{ch for ch in "abracadabra" if ch in "abc"}      # set
(lazy := (line.strip() for line in f))           # generator expression — memory-free
[[r*c for c in range(4)] for r in range(3)]      # nested
[x if x > 0 else 0 for x in data]                # conditional expression inside
flat = [x for row in matrix for x in row]        # flatten (order: outer loop first)
```

### Generators & iterators

```python
def countdown(n):
    while n > 0:
        yield n          # pause here, hand value out
        n -= 1

gen = (x*x for x in range(1_000_000))   # lazy, O(1) memory
next(gen)                               # pull one value
def fib():                              # infinite stream
    a, b = 0, 1
    while True:
        yield a; a, b = b, a + b

# yield from delegates to a sub-generator
def chain_all(*iterables):
    for it in iterables:
        yield from it

# send / close — coroutine-style generators
g = echo(); g.send(None); g.send("hi")
```

Protocol: `iter(obj)` → iterator; `next(it)` → value or `StopIteration`. Anything with `__iter__` is iterable; make your class iterable by defining `__iter__` (generator method is easiest).

### `itertools` — every function

| Function | Yields |
|---|---|
| `count(10, 2)` | 10, 12, 14, … forever |
| `cycle("AB")` | A, B, A, B… |
| `repeat(x, n)` | x, x, x (n times or forever) |
| `chain(a, b)` / `chain.from_iterable(lists)` | Concatenation |
| `compress(data, [1,0,1])` | Keep items where selector truthy |
| `dropwhile(pred, it)` / `takewhile(pred, it)` | Skip/keep until pred fails |
| `filterfalse(pred, it)` | Opposite of builtin filter |
| `groupby(it, key)` | Consecutive groups — **sort first!** |
| `islice(it, 5)` / `islice(it, 2, 10, 2)` | Slicing any iterator |
| `pairwise(it)` (3.10+) | (a,b),(b,c),… sliding pairs |
| `starmap(f, [(1,2),(3,4)])` | f(*args) per item |
| `tee(it, 2)` | Two independent iterators |
| `zip_longest(a, b, fillvalue=0)` | Zip to the longest |
| `product("AB", "12")` | Cartesian product |
| `permutations("ABC", 2)` | Ordered arrangements |
| `combinations("ABC", 2)` | Unordered subsets |
| `combinations_with_replacement("AB", 2)` | With repeats |
| `accumulate([1,2,3])` / `accumulate(xs, operator.mul)` | Running totals/products |

## 16. Functions

### Definitions — the full anatomy

```python
def f(pos_only, /, normal, *args, kw_only=1, **kwargs):
    """Docstring. pos_only is positional-only (the /)."""
    ...

f(1, 2, 3, 4, kw_only=9, anything="goes")
# pos_only=1, normal=2, args=(3,4), kwargs={'anything':'goes'}

def g(a, b=(), /, *, key=None): ...       # / left = positional-only, * right = keyword-only
lambda x, y: x + y                         # expression function
func(*args_list, **kwargs_dict)            # unpacking at call site
```

Defaults are evaluated **once** — the mutable default trap: `def f(x, acc=[])` accumulates forever; use `acc=None` + `acc = [] if acc is None else acc`.

### Closures, decorators, functools

```python
def make_multiplier(n):
    def multiply(x): return x * n          # closes over n
    return multiply

import functools
@functools.cache                            # memoize (3.9+); @lru_cache(maxsize=None) same
def fib(n): return n if n < 2 else fib(n-1) + fib(n-2)

@functools.wraps(f)                         # preserve metadata in custom decorators
def wrapper(*a, **k): ...
```

| `functools` tool | Does |
|---|---|
| `cache` / `lru_cache(maxsize=128, typed=False)` | Memoization |
| `cached_property` | Compute once, store on instance |
| `partial(f, x=1)` | Freeze arguments |
| `reduce(f, iter, init)` | Rolling fold: `reduce(operator.add, xs, 0)` |
| `wraps` | Decorator-preserving decorator |
| `total_ordering` | Define `__eq__`+`__lt__`, get all six comparisons |
| `cmp_to_key(f)` | old-style cmp → sort key |
| `singledispatch` | Function overloading by first-arg type |

### Typing (annotations)

```python
def process(items: list[int], name: str = "x", *,
            limit: int | None = None) -> dict[str, float]: ...

from typing import Optional, Union, Literal, TypedDict, Protocol, Callable, TypeVar, Generic, Any
Vector = list[float]                        # type alias (or `type Vector = list[float]` 3.12+)
T = TypeVar("T")

class Repo(Generic[T]):
    def get(self, id: int) -> T | None: ...

def scale(v: list[float], k: float = 1.0) -> list[float]: return [x * k for x in v]

# gradual typing: hints are NOT enforced at runtime — check with mypy / pyright
```

Common hints: `int str bytes bool float` · `list[T] dict[K,V] set[T] tuple[int, ...]` · `T \| None` (3.10+) · `Literal["a","b"]` · `Callable[[int], str]` · `Iterable/Sequence/Mapping` (accept broad, return precise) · `Any`, `Never`, `Self` (3.11+).

## 17. Classes & OOP

```python
class Animal:
    kingdom = "Animalia"                        # class attribute (shared)
    def __init__(self, name: str, legs: int = 4):
        self.name = name                        # instance attributes
        self.legs = legs
    def speak(self) -> str:
        return "..."
    def __repr__(self):
        return f"Animal({self.name!r})"         # unambiguous (debug) repr
    def __str__(self):
        return f"{self.name} ({self.legs} legs)" # friendly str

class Dog(Animal):                              # inheritance
    def __init__(self, name):
        super().__init__(name, 4)               # call parent init
    def speak(self):                            # override
        return "Woof"

d = Dog("Rex")
isinstance(d, Animal)  → True;  issubclass(Dog, Animal) → True
```

| Concept | Syntax | Notes |
|---|---|---|
| Class attr vs instance | `Dog.kingdom` vs `d.name` | Shared vs per-object |
| Property | `@property` + `@x.setter` + `@x.deleter` | Computed attributes with validation |
| Classmethod | `@classmethod def from_str(cls, s):` | Alternative constructors |
| Staticmethod | `@staticmethod def helper():` | No self/cls — namespaced function |
| `__slots__ = ("a","b")` | Attribute whitelist | Smaller objects, no dict, blocks typos |
| `@dataclass` | See below | Kills boilerplate |
| Multiple inheritance | `class A(B, C)` | MRO via `A.__mro__` / `super()` follows it |
| Mixin | Small base adding one behavior | Convention: suffix `Mixin` |
| Abstract base | `from abc import ABC, abstractmethod` | Force subclasses to implement |
| Protocol | `class Closeable(Protocol): def close(self)->None: ...` | Duck-typed interfaces (static check) |
| Composition > inheritance | `self.engine = Engine()` | Prefer it when tempted by deep trees |

### dataclasses — the boilerplate killer

```python
from dataclasses import dataclass, field

@dataclass
class Point:
    x: float
    y: float = 0.0
    tags: list[str] = field(default_factory=list)   # mutable-safe default

    def dist(self): return (self.x**2 + self.y**2) ** 0.5

p = Point(3, 4)         # __init__ generated
p == Point(3, 4)        # True — __eq__ generated
print(p)                # Point(x=3, y=4) — __repr__ generated
```

Modifiers: `@dataclass(frozen=True)` immutable/hashable · `@dataclass(order=True)` adds `<` etc. · `field(compare=False, repr=False)`. Sister tools: `typing.NamedTuple` (tuple-behavior) and `attrs` (third-party, more features).

## 18. Exceptions

### Full builtin hierarchy

```text
BaseException
├── SystemExit              # sys.exit()
├── KeyboardInterrupt       # Ctrl+C
├── GeneratorExit
└── Exception
    ├── ArithmeticError
    │   ├── ZeroDivisionError
    │   ├── OverflowError
    │   └── FloatingPointError
    ├── AssertionError
    ├── AttributeError
    ├── BufferError
    ├── EOFError
    ├── ImportError
    │   └── ModuleNotFoundError
    ├── LookupError
    │   ├── IndexError
    │   └── KeyError
    ├── MemoryError
    ├── NameError
    │   └── UnboundLocalError
    ├── OSError
    │   ├── FileNotFoundError
    │   ├── FileExistsError
    │   ├── PermissionError
    │   ├── IsADirectoryError / NotADirectoryError
    │   ├── BlockingIOError / InterruptedError
    │   ├── TimeoutError
    │   ├── ConnectionError (Reset/Aborted/Refused)
    │   └── ProcessLookupError / ChildProcessError
    ├── ReferenceError
    ├── RuntimeError
    │   ├── NotImplementedError
    │   └── RecursionError
    ├── StopIteration / StopAsyncIteration
    ├── SyntaxError
    │   └── IndentationError
    │       └── TabError
    ├── SystemError
    ├── TypeError
    ├── ValueError
    │   └── UnicodeError (Decode/Encode/Translate)
    └── Warning (Deprecation, Future, User, RuntimeWarning, …)
```

### Using them properly

```python
try:
    risky()
except (ValueError, KeyError) as e:      # multiple types, bound as e
    log.warning("bad input: %s", e)
except OSError as e:
    if e.errno == 2: ...                  # inspect errno
    raise                                 # re-raise same exception
else:
    print("no exception happened")        # only on success
finally:
    cleanup()                             # always

raise ValueError(f"bad mode: {mode!r}") from cause          # exception chaining
raise TimeoutError("server didn't answer") from None        # hide the chain

class InventoryError(Exception):
    """Custom domain error."""

with contextlib.suppress(FileNotFoundError):
    os.remove("tmp.txt")                  # try/except-pass, but readable
```

**Rules:** catch the **narrowest** exception you can handle; never bare `except:` (it swallows Ctrl+C); don't use exceptions for normal flow control; log the traceback (`logging.exception("msg")` inside except).

## 19. Modules, Packages & Imports

```python
import math                                # whole module
import numpy as np                         # aliased
from datetime import date, timedelta       # names directly
from pathlib import Path as P              # aliased name
from mypkg import submodule                # a submodule
from .sibling import helper                # relative (inside a package)
```

| Concept | Detail |
|---|---|
| Module | Any `.py` file; its name is the filename |
| Package | Folder with `__init__.py` (can be empty); makes `import pkg.mod` work |
| Search order | script dir → `PYTHONPATH` → stdlib → `site-packages` (inspect: `sys.path`) |
| `__name__` | `"__main__"` when run directly, module name when imported — the entry-point idiom |
| `__all__ = ["a","b"]` | What `from mod import *` gives |
| Executed once | A module's body runs at **first import only**; later imports reuse the cached `sys.modules` entry |
| Circular imports | Symptom: `ImportError`/`AttributeError` on package start — fix by restructuring or importing inside functions |
| Namespaced | PEP 420: folders without `__init__.py` are implicit namespace packages |
| Standard layout | `src/myproj/…` + `tests/` + `pyproject.toml` (see §6) |
| `if TYPE_CHECKING:` | Import type-only deps without runtime cost |
| `importlib.import_module("x")` | Dynamic import by string |
| Reload (rare) | `importlib.reload(mod)` |

---
---

## 20. Files & I/O

### `open` — all modes

| Mode | Meaning | Notes |
|---|---|---|
| `r` | Read (default) | Missing → FileNotFoundError |
| `w` | Write, truncate | Creates/destroys |
| `a` | Append | Creates |
| `x` | Exclusive create | Exists → FileExistsError |
| `b` / `t` | Binary / text (default text) | `rb`, `wb`, `r+b`… |
| `+` | Read+write | `r+` no truncate, `w+` truncate |

```python
with open("data.txt", "r", encoding="utf-8", newline="\n") as f:   # ALWAYS with
    text = f.read()                    # whole file
    first = f.readline()
    lines = f.readlines()              # list of lines
for line in f:                         # lazy — best for big files
    process(line.rstrip("\n"))

with open("out.txt", "w", encoding="utf-8") as f:
    f.write("text\n"); f.writelines(lines)
```

`with` guarantees closing even on exceptions. **Always pass `encoding=`** on Windows (default there is locale-dependent — cp1252 landmines). Universal newlines: text mode translates `\r\n`→`\n` automatically.

### `pathlib` — every method that matters

```python
from pathlib import Path
p = Path("docs") / "report" / "final.txt"     # / joins!
```

| Method | Returns |
|---|---|
| `Path.cwd()` / `Path.home()` | Where am I / home dir |
| `p.exists() is_file() is_dir() is_symlink() is_absolute()` | Tests |
| `p.name .stem .suffix .suffixes .parts` | `'final.txt'`, `'final'`, `'.txt'`, `['docs','report','final.txt']` |
| `p.parent` / `p.parents[0..n]` | Up one / ancestors |
| `p.with_name("v2.txt")` / `p.with_suffix(".md")` | Sibling paths |
| `p.resolve()` / `p.absolute()` | Canonical absolute (symlinks resolved) |
| `p.expanduser()` | `~` expansion |
| `p.iterdir()` | Entries of a folder |
| `p.glob("*.log")` / `p.rglob("*.log")` | Pattern match (recursive) |
| `p.mkdir(parents=True, exist_ok=True)` | Create (no errors) |
| `p.rmdir()` / `p.unlink(missing_ok=True)` | Delete dir / file |
| `p.touch()` | Create empty |
| `p.rename(target)` / `p.replace(target)` | Rename / overwrite-rename |
| `p.read_text(encoding="utf-8")` / `p.write_text(s)` | Whole-file shuttle |
| `p.read_bytes()` / `p.write_bytes(b)` | Binary shuttle |
| `p.open("r")` | Built-in open on this path |
| `p.stat()` | `.st_size .st_mtime .st_mtime_ns`… |
| `p.chmod(0o644)` / `p.owner() .group()` | Permissions/ownership |
| `p.samefile(q)` / `p.is_relative_to(base)` / `p.relative_to(base)` | Relations |
| `p.as_posix()` / `p.as_uri()` | String forms |

### `os` / `os.path` / `shutil`

| Call | Does |
|---|---|
| `os.getcwd()` · `os.chdir(p)` · `os.listdir(p)` | Classic trio |
| `os.environ["KEY"]` / `os.getenv("K", default)` | Environment |
| `os.system(cmd)` † | Shell out — prefer `subprocess` |
| `os.path.join(a,b)` · `os.path.exists/abspath/basename/dirname/splitext/getsize/isfile/isdir` | Legacy path ops (pathlib replaces) |
| `os.remove(f)` · `os.mkdir/rmdir` · `os.makedirs(p, exist_ok=True)` | File ops |
| `os.walk(top)` | Yields `(dirpath, dirnames, filenames)` down a tree |
| `os.stat(f).st_size` · `os.rename` · `os.replace` | Metadata/moves |
| `shutil.copy(src,dst)` / `copy2` (metadata) / `copytree` / `rmtree` ⚠ | Copies & deep deletes |
| `shutil.move(src,dst)` | Move |
| `shutil.disk_usage("/")` | Free space |
| `shutil.make_archive("backup","zip",root_dir)` / `unpack_archive` | Zip/tar without zipfile boilerplate |
| `shutil.which("python")` | Locate executable |

### Data formats

```python
import json
json.dumps(obj)  / json.dump(obj, f, indent=2, ensure_ascii=False)   # → str / file
json.loads(s)    / json.load(f)                                      # ← str / file
# tuples→lists, keys must be str, use default= for dates/custom

import csv
with open("t.csv", newline="", encoding="utf-8") as f:
    rows = list(csv.DictReader(f))                 # dicts keyed by header
with open("out.csv", "w", newline="", encoding="utf-8") as f:
    w = csv.DictWriter(f, fieldnames=["a","b"]); w.writeheader(); w.writerows(rows)

import pickle                                  # ⚠ only unpickle data you trust
pickle.dump(obj, open("o.pkl","wb")); obj = pickle.load(open("o.pkl","rb"))

import sqlite3
con = sqlite3.connect("app.db")                # or :memory:
con.execute("CREATE TABLE IF NOT EXISTS t (id INTEGER PRIMARY KEY, name TEXT)")
con.execute("INSERT INTO t(name) VALUES (?)", ("alice",))   # ALWAYS ? params
con.commit(); [r for r in con.execute("SELECT * FROM t WHERE name=?", ("alice",))]
con.row_factory = sqlite3.Row; con.close()

import tempfile, io
tmp = tempfile.NamedTemporaryFile(delete=False); tmp.name
buf = io.StringIO("initial"); buf.seek(0)      # in-memory text file
```

## 21. Concurrency

### Which model for what?

| Workload | Tool |
|---|---|
| Many network waits (HTTP, DB) | `asyncio` |
| Many blocking I/O calls (legacy libs, file ops) | `threading` |
| CPU-bound crunching | `multiprocessing` (or C extensions/numpy) |
| Don't want to choose | `concurrent.futures` thread/process pools |

### `threading`

```python
from threading import Thread, Lock, Event, Semaphore, Condition, local
lock = Lock()
def worker(n):
    with lock:                    # GIL still applies to Python bytecode
        shared.append(n)
threads = [Thread(target=worker, args=(i,)) for i in range(8)]
[t.start() for t in threads]; [t.join() for t in threads]
```

The **GIL**: only one thread runs Python bytecode at a time — threads help I/O concurrency, not CPU parallelism (PEP 703 free-threaded build exists experimentally in 3.13).

### `multiprocessing`

```python
from multiprocessing import Process, Pool, Queue, Pipe
def cube(n): return n * n * n
if __name__ == "__main__":                     # REQUIRED on Windows/macOS spawn
    with Pool() as pool:
        results = pool.map(cube, range(10))    # parallel map
        r = pool.apply_async(cube, (7,)); r.get(timeout=5)
    p = Process(target=worker, args=(1,)); p.start(); p.join()
```

Each process = separate interpreter = true parallel CPU work. Costs: pickling, startup. `multiprocessing.shared_memory` (3.8+) for zero-copy buffers.

### `concurrent.futures` — the friendly face

```python
from concurrent.futures import ThreadPoolExecutor, ProcessPoolExecutor, as_completed
with ThreadPoolExecutor(max_workers=20) as ex:
    futures = {ex.submit(fetch, url): url for url in urls}
    for fut in as_completed(futures):
        try: print(fut.result())
        except Exception as e: print("failed:", futures[fut], e)
pages = list(ex.map(fetch, urls))               # simple parallel map
```

### `asyncio`

```python
import asyncio

async def fetch(name, delay):
    await asyncio.sleep(delay)                  # non-blocking wait
    return f"{name} done"

async def main():
    # sequential
    a = await fetch("a", 1)
    # concurrent — gather (results in order)
    results = await asyncio.gather(fetch("b", 2), fetch("c", 1), return_exceptions=True)
    # structured concurrency (3.11+)
    async with asyncio.TaskGroup() as tg:
        t1 = tg.create_task(fetch("d", 1))
        t2 = tg.create_task(fetch("e", 2))       # one fails → all cancelled
    # timeout
    try:
        await asyncio.wait_for(fetch("f", 10), timeout=2)
    except TimeoutError: pass

asyncio.run(main())                              # THE entry point
```

| API | Purpose |
|---|---|
| `asyncio.run(coro)` | Run the top-level coroutine |
| `asyncio.gather(*aws)` | Concurrent, ordered results |
| `asyncio.TaskGroup` (3.11+) | Structured, auto-cancel on error |
| `asyncio.create_task(c)` | Schedule without awaiting immediately |
| `asyncio.wait_for(aw, t)` / `asyncio.timeout(t)` (3.11+) | Time limits |
| `asyncio.sleep(d)` | Non-blocking delay |
| `asyncio.Queue` / `Lock` / `Event` / `Semaphore` | Coordination primitives (async versions) |
| `asyncio.as_completed(aws)` | Iterate as they finish |
| `asyncio.to_thread(func, …)` | Push blocking call to a thread |
| `asyncio.start_server / open_connection` | Async sockets |

Libraries must be async-native (`aiohttp`, `httpx` async mode). `await` only inside `async def`. One event loop per process.

## 22. Standard Library Essentials

### `datetime` — the complete kit

```python
from datetime import datetime, date, time, timedelta, timezone
now = datetime.now()                      # local, naive
utc  = datetime.now(timezone.utc)         # TIMEZONE-AWARE — prefer for real code
datetime.fromisoformat("2026-08-30T14:30:00+02:00")   # parse ISO (3.11+: most formats)
dt = datetime.strptime("30/08/2026", "%d/%m/%Y")      # parse any format
dt.strftime("%Y-%m-%d %H:%M")                         # format out
dt + timedelta(days=7, hours=3)                       # arithmetic
(dt2 - dt1).days / .total_seconds()                   # differences
dt.timestamp() ; datetime.fromtimestamp(1760000000)   # epoch shuttle
date.today() ; dt.date() ; dt.year .month .day .hour .weekday()  # Monday=0 / isoweekday()
```

`strftime` directives: `%Y %m %d %H %M %S` big four · `%y` 2-digit year · `%I %p` 12-hour + AM/PM · `%j` day of year · `%a %A %b %B` names · `%f` microseconds · `%z %Z` timezone · `%s`† · `%U %W %V` weeks · `%c %x %X` locale · `%%` literal. Gotcha: comparing naive and aware datetimes raises TypeError — normalize with `dt.astimezone()`. Third-party `dateparser`/`pendulum` for human formats ("3 days ago").

### `collections`

| Tool | Use |
|---|---|
| `Counter("mississippi").most_common(3)` | Frequency counting |
| `defaultdict(list)` | Dict with auto-factory — kills `setdefault` boilerplate |
| `deque(maxlen=n)` | Fast append/pop both ends — sliding windows, queues |
| `namedtuple("P", "x y")` | Tuple with names |
| `OrderedDict` † | Ordered since 3.7 plain dict; still useful for move_to_end |
| `ChainMap(a, b)` | Layered lookup (defaults over overrides) |
| `UserDict/List/String` | Base classes for custom containers |

### `random`, `math`, `statistics`, `secrets`

| Call | Returns |
|---|---|
| `random.random()` / `randint(1,6)` / `randrange(0,10,2)` | Float [0,1) / inclusive int / step |
| `random.choice(seq)` / `choices(seq, k=5, weights=…)` / `sample(seq, k)` | Picks (no/with replacement) |
| `random.shuffle(list)` | In-place |
| `random.seed(42)` | Reproducible |
| `math.ceil floor fabs factorial gcd lcm sqrt cbrt(3.11+)` | Basics |
| `math.pi e tau inf nan` · `math.log(x, b)` `log2 log10` `exp` | Constants/logs |
| `math.isclose(a,b,rel_tol=1e-9)` | Float-safe compare |
| `statistics.mean median mode stdev variance quantiles` | Stats |
| `secrets.token_hex(32)` / `token_urlsafe(16)` / `randbelow(n)` | **Crypto-safe** randomness |
| `secrets.compare_digest(a,b)` | Constant-time compare |

⚠ `random` is NOT for security — use `secrets`. Random ints in hot loops: `random.Random(seed)` instance avoids global lock.

### Hashing & encoding

| Call | Purpose |
|---|---|
| `hashlib.sha256(b).hexdigest()` (`md5†` `sha1†` `sha512` `blake2b` `sha3_256`) | Digests — verify downloads, fingerprint |
| `hashlib.file_digest(open(f,'rb'), 'sha256')` (3.11+) | Streamed file hash |
| `hmac.new(key, msg, 'sha256').hexdigest()` | Signed messages |
| `base64.b64encode(b)` / `b64decode` / `urlsafe_b64*` | Transport encoding (not encryption!) |
| `uuid.uuid4()` | Random UUID; `uuid1()` host-based; `uuid5(ns, name)` deterministic |

### `subprocess` — run anything

```python
import subprocess
r = subprocess.run(["ping", "-n", "1", "example.com"], capture_output=True,
                   text=True, timeout=10, check=False)
r.returncode, r.stdout, r.stderr
subprocess.run("echo hi > f.txt", shell=True)             # ⚠ shell=True = injection risk
subprocess.run(["python", "script.py"], input="y\n", text=True, check=True)
```

| Param | Meaning |
|---|---|
| `args` list | Program + args (no shell parsing — safe) |
| `capture_output=True` | Collect stdout+stderr |
| `text=True` | Decode to str (else bytes) |
| `input="…"` | Feed stdin |
| `check=True` | Non-zero → `CalledProcessError` |
| `timeout=30` | Kill after 30 s (`TimeoutExpired`) |
| `cwd=`, `env={**os.environ, "K":"v"}` | Working dir / environment |
| `Popen(…)` | Low-level streaming (`p.stdout.readline()`, `p.communicate()`) |

Legacy: `os.system` † · `os.popen` † — migrate both to `subprocess`.

### `argparse` — full walkthrough

```python
import argparse

p = argparse.ArgumentParser(
    prog="tool", description="Do the thing",
    epilog="Enjoy.")
p.add_argument("src", help="source file")                       # positional
p.add_argument("dst", nargs="?", default="out.txt")             # optional positional
p.add_argument("-n", "--dry-run", action="store_true")          # flag
p.add_argument("-v", "--verbose", action="count", default=0)    # -vvv → 3
p.add_argument("--limit", type=int, default=10)                 # typed option
p.add_argument("--mode", choices=["fast","safe"], default="safe")
p.add_argument("--tags", action="append")                       # repeatable → list
p.add_argument("--log", type=argparse.FileType("w"))            # opens the file!
p.add_argument("--retries", metavar="N", type=int, default=3)
sub = p.add_subparsers(dest="cmd", required=True)
p_init = sub.add_parser("init", help="create config")
p_init.add_argument("--force", action="store_true")
p_push = sub.add_parser("push", help="upload")
p_push.add_argument("target")

args = p.parse_args()          # --help auto-generated from all of the above
```

| Concept | Detail |
|---|---|
| `nargs` | `N` exactly · `?` 0-or-1 · `*` any list · `+` at least one |
| `action` | `store` · `store_true/false/const` · `append` · `count` · `extend` · custom Action class |
| `type` | Any callable — `int`, `float`, `Path`, `datetime.fromisoformat` |
| `default` + `required=True` | Optionality control |
| `dest` | Attribute name (from long option by default) |
| `parse_known_args()` | Ignore unknown (wrapper scripts) |
| `args = p.parse_args(["init","--force"])` | Testing parsers programmatically |

Alternatives: `typer` (type-hint driven, pretty) and `click` (decorator based) — argparse needs zero dependencies.

### `logging` — full walkthrough

```python
import logging
logging.basicConfig(
    level=logging.INFO,
    format="%(asctime)s %(levelname)-8s %(name)s: %(message)s",
    datefmt="%Y-%m-%d %H:%M:%S",
    filename="app.log",          # omit → stderr
)
log = logging.getLogger("payroll")           # per-module loggers: logging.getLogger(__name__)
log.debug("detail %s", item)                 # lazy % formatting — never f-strings in hot paths
log.info("processed %d rows", n)
log.warning("deprecated call")
log.error("failed: %s", err)
log.exception("boom")                        # ERROR + traceback (in except block)
```

| Level | Numeric | Use |
|---|---|---|
| `DEBUG` | 10 | Everything while developing |
| `INFO` | 20 | Normal milestones |
| `WARNING` | 30 | Default level — surprising but recoverable |
| `ERROR` | 40 | Operation failed |
| `CRITICAL` | 50 | App going down |

Advanced: handlers (`StreamHandler`, `FileHandler`, `RotatingFileHandler(maxBytes, backupCount)`, `SMTPHandler`), `Formatter`, `dictConfig` from YAML/JSON, `logging.config.dictConfig({...})`, propagate/filter per logger. Rule: libraries log, **never** configure basicConfig inside a library — only in the app entry point.

### Networking quick hits

| Call | Purpose |
|---|---|
| `urllib.request.urlopen(url)` | Stdlib HTTP GET (clunky but zero-dep) |
| `pip install requests` → `requests.get(url, timeout=5, headers=…)`; `r.json() r.status_code r.raise_for_status()` | The human API |
| `httpx` | requests-compatible + async + HTTP/2 |
| `socket.create_connection((host, port), timeout=5)` | Raw TCP |
| `email/smtplib` | MIME building + SMTP send (`smtplib.SMTP(host).send_message(msg)`) |
| `webbrowser.open(url)` | Open browser |

### Archives, glob, platform

| Call | Purpose |
|---|---|
| `zipfile.ZipFile("a.zip")` → `.namelist() .extractall(dir) .read(name)` · `ZipFile("a.zip","w").write(f)` | Zip I/O |
| `tarfile.open("a.tar.gz", "r:gz")` | Tar I/O |
| `glob.glob("data/*.csv", recursive=True)` · `glob.iglob` | Wildcard files (pathlib `glob` usually nicer) |
| `platform.system() .machine() .python_version()` | OS/CPU/Py detection |
| `os.name` (`"nt"`/`"posix"`) · `sys.platform` (`win32`/`linux`/`darwin`) | Platform branches |
| `sys.argv` · `sys.exit(code)` · `sys.stdin/stdout/stderr` · `sys.modules` · `sys.path` | System handles |
| `time.time() time.sleep(s) time.perf_counter()` | Clocks — perf_counter for timing! |
| `shelve.open("data")` | Pickle-backed dict on disk |

---
---

# PART 3 — HANDS-ON TUTORIALS

## T1. Your First Hour

**Goal:** variables → data → loops → functions, ending with two tiny real programs.

```python
# Step 1 — the calculator soul of Python (REPL: >>> means type it live)
2 + 2, 7 / 2, 7 // 2, 7 % 2, 2 ** 10          # (4, 3.5, 3, 1, 1024)

# Step 2 — variables & types (dynamic: names are labels, not boxes)
width, height = 3, 4
area = width * height
type(area)                                     # <class 'int'>

# Step 3 — strings & f-strings
name = "Ada"
print(f"{name} computed area={area}")

# Step 4 — lists and loops
temps = [21, 25, 19, 30, 27]
for t in temps:
    print("hot" if t >= 25 else "mild", t)
print("avg:", sum(temps) / len(temps))

# Step 5 — functions
def to_f(c): return c * 9 / 5 + 32
print([to_f(t) for t in temps])

# Step 6 — dict as a tiny database
people = {"ada": 36, "alan": 41}
people["grace"] = 45
for who, age in sorted(people.items()):
    print(f"{who:>6}: {age}")

# Step 7 — program 1: number guessing game
import random
secret = random.randint(1, 100)
while (guess := int(input("Guess: "))) != secret:
    print("higher" if guess < secret else "lower")
print("Correct!")

# Step 8 — program 2: word counter
text = input("Sentence: ")
counts = {}
for word in text.lower().split():
    counts[word] = counts.get(word, 0) + 1
print(sorted(counts.items(), key=lambda kv: -kv[1]))
```

**Checkpoint:** you can store data (list/dict), repeat work (for/while), package logic (def), and read input. That's 80 % of daily Python.

## T2. Parse a Log File → CSV Report

```python
# parse access logs like: 2026-08-30 12:01:02 ERROR payment failed id=771
import re, csv
from collections import Counter
from pathlib import Path

log_re = re.compile(r"(?P<date>\d{4}-\d{2}-\d{2}) (?P<time>\d{2}:\d{2}:\d{2}) "
                    r"(?P<level>INFO|WARNING|ERROR) (?P<msg>.*)")

rows, level_counts = [], Counter()
for line in Path("app.log").read_text(encoding="utf-8").splitlines():
    if m := log_re.match(line):
        rows.append(m.groupdict())
        level_counts[m["level"]] += 1

with open("report.csv", "w", newline="", encoding="utf-8") as f:
    w = csv.DictWriter(f, fieldnames=["date", "time", "level", "msg"])
    w.writeheader(); w.writerows(rows)

print("levels:", dict(level_counts))
print("errors on:", {r["date"] for r in rows if r["level"] == "ERROR"})
```

Teaches: `re` named groups, walrus, `Counter`, `pathlib`, `csv.DictWriter`.

## T3. Consume Any REST API (JSON)

```python
import requests

def get_json(url, **params):
    r = requests.get(url, params=params, timeout=10)
    r.raise_for_status()
    return r.json()

data = get_json("https://api.github.com/repos/python/cpython/events", per_page=5)
for ev in data:
    print(f"{ev['type']:<22} {ev['actor']['login']:<20} {ev['repo']['name']}")

# POST with auth:
# requests.post(url, json={"key": "value"}, headers={"Authorization": f"Bearer {token}"})
```

Teaches: HTTP verbs, params/timeout, raise_for_status, JSON navigation (`['type']`), and the habit of wrapping API calls in small functions. Retry logic: `HTTPAdapter(max_retries=3)` in a `requests.Session`.

## T4. Build a Real CLI App (`argparse`)

```python
"""todo.py — a tiny task manager."""
import argparse, json
from pathlib import Path

DB = Path.home() / ".todo.json"

def load():
    return json.loads(DB.read_text()) if DB.exists() else []
def save(tasks): DB.write_text(json.dumps(tasks, indent=2))

def main():
    p = argparse.ArgumentParser(description="Tiny todo")
    sub = p.add_subparsers(dest="cmd", required=True)
    a = sub.add_parser("add");    a.add_argument("task", help="task text")
    d = sub.add_parser("done");   d.add_argument("n", type=int, help="task number")
    sub.add_parser("list", help="show tasks")
    args = p.parse_args()

    tasks = load()
    match args.cmd:
        case "add":  tasks.append({"task": args.task, "done": False}); save(tasks)
        case "done": tasks[args.n - 1]["done"] = True; save(tasks)
        case "list":
            for i, t in enumerate(tasks, 1):
                print(f"{'✓' if t['done'] else '·'} {i}. {t['task']}")

if __name__ == "__main__":
    main()
```

Run: `python todo.py add "Ship the report"` → `python todo.py list` → `python todo.py done 1`.
Next level: convert with `typer` (add type hints, get `--help` for free) and install as a command with `pipx install` after adding a `[project.scripts]` entry (§6).

## T5. OOP with Dataclasses — an Inventory Manager

```python
from dataclasses import dataclass, field
from enum import Enum

class Condition(Enum):
    NEW = "new"; USED = "used"; BROKEN = "broken"

@dataclass(order=True)
class Item:
    sort_index: float = field(init=False, repr=False)
    sku: str = ""
    name: str = ""
    price: float = 0.0
    condition: Condition = Condition.NEW
    tags: list[str] = field(default_factory=list)

    def __post_init__(self):
        self.sort_index = -self.price          # highest price first

class Inventory:
    def __init__(self): self._items: dict[str, Item] = {}
    def add(self, item: Item): self._items[item.sku] = item
    def total_value(self) -> float:
        return sum(i.price for i in self._items.values() if i.condition != Condition.BROKEN)
    def find(self, query: str) -> list[Item]:
        q = query.lower()
        return [i for i in self._items.values() if q in i.name.lower() or q in " ".join(i.tags)]

inv = Inventory()
inv.add(Item(sku="A1", name="Keyboard", price=79.9, tags=["input"]))
inv.add(Item(sku="A2", name="Monitor", price=349, condition=Condition.USED))
print(inv.total_value(), inv.find("monitor"))
```

Teaches: `@dataclass(order=True)`, `field(init=False)` + `__post_init__`, `Enum`, private-by-convention attributes, type-hinted composition.

## T6. Package & Publish a Library to PyPI

```bash
# 1. Layout
mylib/
├── pyproject.toml      # from §6 — name, version, deps, [project.scripts]
├── README.md
├── src/mylib/__init__.py
└── tests/test_mylib.py

# 2. Local sanity
python -m venv .venv && source .venv/bin/activate
pip install -e . && mylib-cli --help          # entry point works?

# 3. Build & validate
pip install build twine
python -m build
twine check dist/*

# 4. Rehearse on TestPyPI, then the real thing
twine upload --repository testpypi dist/*
pip install -i https://test.pypi.org/simple/ mylib && python -c "import mylib"
twine upload dist/*                            # needs a PyPI API token
```

Checklist before upload: unique name, version bumped, README renders (`twine check`), license present, no secrets in the sdist. Every re-upload of the same version is rejected — bump first.

## T7. Test Like a Pro with pytest

```python
# tests/test_math.py
import pytest
from mylib import add, divide, load_config

def test_add_ints():
    assert add(2, 3) == 5

@pytest.mark.parametrize("a,b,out", [(0,0,0), (-1,1,0), (100,1,101)])
def test_add_many(a, b, out):
    assert add(a, b) == out

def test_divide_by_zero():
    with pytest.raises(ZeroDivisionError):
        divide(1, 0)

@pytest.fixture
def config(tmp_path):
    cfg = tmp_path / "c.ini"; cfg.write_text("[main]\nkey=1\n")
    return load_config(cfg)

def test_config(config):
    assert config["main"]["key"] == "1"

def test_output(capsys):
    print("hi"); assert capsys.readouterr().out == "hi\n"
```

```bash
pytest -v --durations=3
pytest --lf
pytest --cov=mylib --cov-report=term-missing
```

Teaches: one concept per test, AAA (Arrange-Act-Assert), fixtures over setup boilerplate, parametrize over copy-paste, raises-testing, coverage flags.

## T8. Automate the Boring Stuff

```python
# A — rename & sort a folder of photos by EXIF-less mtime
from pathlib import Path
from datetime import datetime
for p in Path("dump").iterdir():
    if p.is_file():
        stamp = datetime.fromtimestamp(p.stat().st_mtime).strftime("%Y-%m/%Y%m%d_%H%M%S")
        target = Path("sorted") / f"{stamp}{p.suffix}"
        target.parent.mkdir(parents=True, exist_ok=True)
        p.rename(target)

# B — Excel → cleaned Excel (pip install openpyxl pandas)
import pandas as pd
df = pd.read_excel("sales.xlsx", sheet_name="Q3")
clean = (df.dropna(subset=["amount"])
           .assign(total=lambda d: d.amount * d.qty)
           .groupby("region", as_index=False)["total"].sum())
clean.to_excel("sales_summary.xlsx", index=False)

# C — send an email report (stdlib)
import smtplib
from email.message import EmailMessage
msg = EmailMessage()
msg["From"], msg["To"], msg["Subject"] = "me@x.com", "boss@x.com", "Weekly report"
msg.set_content(open("report.txt").read())
with smtplib.SMTP("smtp.example.com", 587) as s:
    s.starttls(); s.login("me@x.com", "app-password"); s.send_message(msg)

# D — watch a folder for new files
import time
seen = set()
while True:
    for p in Path("inbox").glob("*.csv"):
        if p not in seen:
            seen.add(p); print("new:", p); # process(p)
    time.sleep(2)
```

## T9. Async — a Concurrent Downloader

```python
import asyncio, aiohttp, time

URLS = [f"https://httpbin.org/delay/{d}" for d in (1, 1, 1, 1, 1)]

async def fetch(session, url):
    async with session.get(url, timeout=aiohttp.ClientTimeout(total=15)) as r:
        return url, r.status

async def main():
    async with aiohttp.ClientSession() as session:
        async with asyncio.TaskGroup() as tg:                    # 3.11+
            tasks = [tg.create_task(fetch(session, u)) for u in URLS]
    for t in tasks:
        print(t.result())

start = time.perf_counter()
asyncio.run(main())
print(f"5 requests in {time.perf_counter() - start:.1f}s (sequential would be ~5s)")
```

`pip install aiohttp` first. Same pattern with threads for blocking libraries: `ThreadPoolExecutor` + `fetch` (§21). Teaches: async/await, sessions, TaskGroup, timeouts, and measuring speedups honestly.

## T10. Debug & Profile Like a Detective

```bash
# 1 — reproduce under pdb
python -m pdb app.py input.csv
(Pdb) b app.py:42            # break where it goes wrong
(Pdb) c                      # run to it
(Pdb) p rows[:3]             # inspect
(Pdb) pp {r["id"]: r for r in rows}
(Pdb) w                      # how did we get here?
(Pdb) interact               # full REPL with all locals

# 2 — or post-mortem the last crash
python -i app.py
>>> import pdb; pdb.pm()

# 3 — find the hotspot
python -m cProfile -s cumtime app.py | head -25
# or: python -X importtime -c "import app" 2>&1 | sort -t'|' -k2 -n | tail
```

Method: (1) make it fail deterministically (smallest input), (2) read the traceback **bottom-up** — last frame is where it died, walk up for who caused it, (3) inspect state with pdb rather than guessing, (4) profile before optimizing, (5) after fixing: add the regression test (T7).

---
---

# PART 4 — APPENDICES

## Appendix A — A–Z Command & Tool Index (Part 1)

| | Tools |
|---|---|
| **B** | `black` §8 · `build` §6 · `bandit` §8 |
| **C** | `conda`/`mamba` §4 · `coverage` §7 |
| **F** | `flake8` §8 |
| **I** | `ipython` §0.4 · `isort` §8 · `ipdb`/`pudb` §9 |
| **J** | `jupyter lab/notebook/console/nbconvert/kernelspec` §10 |
| **M** | `mypy` §8 · `mamba` §4 |
| **P** | `python` §1 (all flags) · `py` launcher §2 · `pip` §3 · `pipx` §4 · `poetry` §4 · `pre-commit` §8 · `pylint` §8 · `pydoc` §5,§0.6 · `pdb` §9 · `pstats` §9 |
| **R** | `ruff` §8 |
| **T** | `twine` §6 · `timeit` §5,§9 · `tracemalloc` §9 |
| **U** | `uv` §4 (venv/pip/add/sync/run/tool/uvx) · `unittest` §7 |
| **V** | `venv` §4 · `virtualenv` §4 |

`python -m` modules (§5): `http.server` · `json.tool` · `timeit` · `cProfile` · `pdb` · `pydoc` · `zipfile` · `tarfile` · `base64` · `compileall` · `ensurepip` · `site` · `sysconfig` · `unittest` · `venv` · `webbrowser` · `ast` · `dis` · `this`.

## Appendix B — All Built-in Functions

| | | | |
|---|---|---|---|
| `abs(x)` | absolute value | `hash(o)` | identity-based hash |
| `aiter(x)` / `anext(x)` (3.10+) | async iteration | `help([x])` | interactive docs |
| `all(it)` / `any(it)` | every/any truthy | `hex(i)` / `oct(i)` / `bin(i)` | base strings |
| `ascii(o)` | repr, non-ASCII escaped | `id(o)` | identity int |
| `bin(i)` | `'0b…'` | `input([prompt])` | read a string |
| `bool(x)` | truthiness | `int(x[, base])` | parse/convert |
| `breakpoint()` | drop into pdb | `isinstance(o, T)` | type test (tuple ok) |
| `bytearray(x)` / `bytes(x)` | mutable/immutable bytes | `issubclass(A, B)` | class test |
| `callable(o)` | has `__call__` | `iter(it)` / `next(it[,d])` | iterator protocol |
| `chr(i)` / `ord(c)` | code ↔ character | `len(x)` | size |
| `classmethod(f)` | classmethod wrapper | `list(it)` / `tuple(it)` | sequences |
| `compile(src,…)` | source → code object | `locals()` / `globals()` | namespace dicts |
| `complex(re,im)` | complex number | `map(f, *its)` | lazy transform |
| `delattr(o,n)` / `getattr(o,n[,d])` / `setattr(o,n,v)` / `hasattr(o,n)` | attribute tools | `max(it[,key])` / `min(it[,key])` | extremes |
| `dict(**kw)` | new dict | `memoryview(b)` | zero-copy view |
| `dir([o])` | name list | `object()` | base of everything |
| `divmod(a,b)` | `(a//b, a%b)` | `oct(i)` | `'0o…'` |
| `enumerate(it, s=0)` | index+value | `open(path,…)` | file handle |
| `eval(e)` / `exec(e)` ⚠ | run dynamic code | `pow(b,e[,m])` | power (fast mod) |
| `filter(f, it)` | keep matching | `print(*a, sep,end,file,flush)` | output |
| `float(x)` | parse float | `property(fget,…) ` | descriptor |
| `format(v, spec)` | `__format__` | `range(a,b,s)` | lazy ints |
| `frozenset(it)` | immutable set | `repr(o)` | debug string |
| `reversed(seq)` | reverse iterator | `round(x[,n])` | banker's rounding |
| `set(it)` | new set | `slice(a,b,s)` | slice object |
| `sorted(it,key,rev)` | new sorted list | `staticmethod(f)` | static wrapper |
| `str(x)` | string form | `sum(it[,start])` | total |
| `super()` | next-in-MRO proxy | `type(o)` / `type(n,b,d)` | type of / build class |
| `vars([o])` | `__dict__` | `zip(*its, strict=False)` | parallel iteration |
| `exit()` / `quit()` | leave REPL (never in scripts) | `__import__(n)` | low-level import |

## Appendix C — Dunder Methods Protocol Table

| Protocol | Methods | Triggered by |
|---|---|---|
| Construction | `__new__` `__init__` `__del__` | creation / destruction (GC) |
| String forms | `__repr__ __str__ __bytes__ __format__` | `repr()` `print()` `bytes()` f-strings |
| Comparison | `__eq__ __ne__ __lt__ __le__ __gt__ __ge__` | `== != < <= > >=`, `sorted` |
| Hashing | `__hash__` | `hash()`, dict/set keys (pair with `__eq__`) |
| Truth | `__bool__` `__len__` | `if x:`, `bool()` |
| Attribute access | `__getattr__ __getattribute__ __setattr__ __delattr__ __dir__` | dot access, `dir()` |
| Descriptors | `__get__ __set__ __delete__ __set_name__` | property/class machinery |
| Containers | `__len__ __getitem__ __setitem__ __delitem__ __contains__ __missing__` | `len()` `[]` `in` |
| Iteration | `__iter__ __next__ __reversed__ __length_hint__` | `for`, `iter()`, unpacking |
| Callable | `__call__` | `obj()` |
| Context manager | `__enter__ __exit__` | `with` |
| Arithmetic | `__add__ __sub__ __mul__ __truediv__ __floordiv__ __mod__ __pow__ __matmul__ @` | operators |
| Reflected | `__radd__ __rsub__ …` | right operand implements |
| In-place | `__iadd__ __isub__ …` | `+=` and friends |
| Unary | `__neg__ __pos__ __abs__ __invert__` | `-x +x abs(x) ~x` |
| Conversions | `__int__ __float__ __complex__ __index__ __bool__` | `int()`, slicing indices |
| Types | `__class__ __mro__ __bases__ __slots__ __dict__` | introspection |
| Path/name | `__name__ __qualname__ __module__ __file__` | module/function identity |
| Entry point | `__main__` | `if __name__ == "__main__"` |
| Async | `__aiter__ __anext__ __aenter__ __aexit__` | `async for` / `async with` |

## Appendix D — Format Spec Quick Table

| Want | Spec | Example → result |
|---|---|---|
| 2 decimals | `.2f` | `f"{3.14159:.2f}"` → `3.14` |
| Thousands | `,` | `f"{1234567:,}"` → `1,234,567` |
| Percent | `.1%` | `f"{0.856:.1%}"` → `85.6%` |
| Hex/oct/bin | `x` `o` `b` (`#x` prefixed) | `f"{255:#x}"` → `0xff` |
| Padding right/left/center | `>10` `<10` `^10` | `f"{'ab':^6}"` → `' ab  '` |
| Zero pad | `08d` | `f"{42:08d}"` → `00000042` |
| Sign always | `+d` | `f"{5:+d}"` → `+5` |
| Exponent | `e` | `f"{12345.6:e}"` → `1.234560e+04` |
| Significant digits | `.3g` | `f"{12345.6:.3g}"` → `1.23e+04` |
| Debug dump | `=` | `f"{price=}"` → `price=19.99` |
| repr | `!r` | `f"{'a'!r}"` → `"'a'"` |
| nested width | `{v:>{w}}` | dynamic width from variable |
| datetime | `:%Y-%m-%d` | inline date formatting |

## Appendix E — The Exceptions You'll Actually Meet

| Exception | Typical cause → fix |
|---|---|
| `SyntaxError` | Typo/unclosed bracket — read the caret line |
| `IndentationError`/`TabError` | Mixed tabs+spaces — configure editor to spaces |
| `NameError` / `UnboundLocal` | Typo'd or pre-import use; missing `global`/`nonlocal` |
| `TypeError` | Wrong types (`"a"+1`) or wrong arg count — check signatures |
| `ValueError` | Right type, bad value: `int("abc")` — validate first |
| `IndexError` / `KeyError` | Out of range / missing key — `.get()`, guard lengths |
| `AttributeError` | `'NoneType' has no attribute x` — a function returned None (missing return!) |
| `ImportError`/`ModuleNotFoundError` | Not installed / wrong venv / wrong name — `pip install`, check `sys.path` |
| `FileNotFoundError` / `PermissionError` | Wrong cwd, relative paths — use absolute `Path`s; run as admin |
| `ZeroDivisionError` | Guard denominators |
| `StopIteration` leaked | `next()` past end outside a for-loop — give `next(it, default)` |
| `RecursionError` | Missing base case — rewrite iteratively |
| `UnicodeDecodeError` | Read bytes as utf-8 of a non-utf8 file — pass `encoding=` / `errors=` |
| `TypeError: can't pickle` | Lambdas/local objects crossing process boundaries |
| `OSError errno 22` | Invalid path chars (`:` in Windows filenames!) |

Full hierarchy tree: §18. Custom errors: subclass `Exception`, name it `SomethingError`.

## Appendix F — One-Liner Cookbook

```python
# Files & data
python -c "import json;print(json.dumps(json.load(open('x.json')),indent=2))"   # pretty JSON
sorted(paths, key=lambda p: p.stat().st_size)[-1]      # biggest file
Path("f.txt").read_text().count("ERROR")               # occurrences
[*{line.split(',')[0] for line in open('t.csv')}]      # unique first column

# Collections
sorted(d.items(), key=lambda kv: -kv[1])               # dict by value desc
[x for x in xs if x not in seen]                       # dedupe, keep order
list(zip(*matrix))                                     # transpose
max(words, key=len)                                    # longest word
collections.Counter(nums).most_common(1)[0]            # mode

# Strings
", ".join(sorted(set(names)))                          # unique, sorted, comma'd
s.title() ; s.capitalize() ; " ".join(w.capitalize() for w in s.split())
any(p in text.lower() for p in ["err","fail"])         # keyword alarm
str(int("ff",16)) ; f"{255:08b}"                       # base conversions

# Clever stdlib
python -m http.server 8000                             # share this folder
python -m json.tool messy.json                         # validate JSON
python -m zipfile -e app.zip out/                      # unzip anything
sum(a[1]*b[1] for a,b in zip(prices,qtys))             # dot product
__import__("sys").exit(1)                              # last-resort inline exit
```

## Appendix G — Traceback Decoding, Errors & Best Practices

**Reading a traceback (bottom-up):**

```text
Traceback (most recent call last):        ← read DOWN to find your code…
  File "app.py", line 10, in <module>     ← your entry: process(invoice)
  File "lib.py", line 4, in process
    total = sum(row["qty"] for row in rows)
  File "lib.py", line 4, in <genexpr>
KeyError: 'qty'                           ← …the LAST line names the disease
```

1. **Last line** = exception type + message — the actual problem. 2. Walk **up** the frames to the first file that is *yours* — that's where to look. 3. The nearest source line shows the crashing expression. Search the exact last line + "python" when stuck.

**Best-practice checklist**
1. `python -m venv .venv` per project — always; commit `requirements.txt`/lock file, never the env.
2. `python -m pip …` inside the env; `pipx` for tools.
3. `with open(...) as f:` and explicit `encoding="utf-8"` — every time.
4. f-strings for humans, `logging` (not print) for operations, `--help` for every script.
5. Type-hint public functions; run `ruff check` + `mypy` in CI; test with `pytest`.
6. Prefer `pathlib` over `os.path`; `subprocess.run(list, check=True, timeout=)` over `shell=True`.
7. Exceptions: catch narrow, `raise` to re-throw, `logging.exception` to record.
8. Functions do one thing; dataclasses over bare dicts at API boundaries; comprehensions over map/filter when readable.
9. Profile before optimizing (`cProfile`, `timeit`) — 90 % of slowness is I/O or an accidental O(n²).
10. Pin versions in production (`==`/lock), float ranges (`>=x,<y`) in libraries.

## Appendix H — Every Python Library: Complete Standard Library + Essential Third-Party

> **Scope:** the standard library below is the **complete** set of public, documented modules (Python 3.12/3.13) — organized by purpose. Third-party can never be "complete" (PyPI hosts **600,000+ projects**), so Part 2 of this appendix is the curated essential set by domain — the libraries actually worth knowing, chosen by ecosystem share and quality.

### H.1 The Standard Library — complete catalog by category

**Runtime, interpreter & introspection**

| Module | What it does |
|---|---|
| `sys` | Interpreter handles: argv, path, exit, stdout, modules, version |
| `sysconfig` | Build/interpreter configuration & paths |
| `builtins` | The built-in functions/names namespace |
| `__main__` | Entry-point machinery (`if __name__ == "__main__"`) |
| `warnings` | Warning control (`-W`, ` DeprecationWarning`) |
| `atexit` | Run functions on interpreter shutdown |
| `gc` | Garbage collector control & stats |
| `inspect` | Live objects: signatures, source, stack frames |
| `site` | Startup path setup (`site-packages`, `.pth`) |
| `stat` | File-mode bit constants & interpreters |
| `contextlib` | `with` helpers: `contextmanager`, `suppress`, `closing` |
| `abc` | Abstract base classes (`ABC`, `abstractmethod`) |
| `dataclasses` | Boilerplate-free classes (`@dataclass`) |
| `types` | Dynamic type creation, `SimpleNamespace`, `NoneType` |
| `copy` | Shallow/deep copies |

**Text processing**

| Module | What it does |
|---|---|
| `string` | Constants, `Template`, `Formatter` |
| `re` | Regular expressions |
| `difflib` | Diff/similarity (`SequenceMatcher`, `get_close_matches`) |
| `textwrap` | Wrap/fill/dedent paragraphs |
| `unicodedata` | Unicode names, categories, normalization |
| `stringprep` | IDNA string preparation |
| `readline` | Line editing/history (Unix; `pyreadline3` on Windows) |
| `rlcompleter` | Tab-completion for the REPL |
| `codecs` | Encoders/decoders registry, `open` codecs |

**Binary data**

| Module | What it does |
|---|---|
| `struct` | Pack/unpack C structs to/from bytes |
| `binascii` | hex/base64/uudecode primitives |

**Data types & containers**

| Module | What it does |
|---|---|
| `datetime` | Dates, times, time zones, arithmetic |
| `zoneinfo` (3.9+) | IANA time-zone database |
| `calendar` | Calendar generation/formatting |
| `collections` | `Counter`, `defaultdict`, `deque`, `namedtuple`, `ChainMap` |
| `collections.abc` | Abstract base classes: `Iterable`, `Mapping`, … |
| `heapq` | Min-heap priority queue |
| `bisect` | Binary search in sorted lists |
| `array` | Compact typed numeric arrays |
| `weakref` | Garbage-collectable references |
| `enum` | Enumerations (`Enum`, `IntEnum`, `StrEnum` 3.11+) |
| `graphlib` (3.9+) | Topological sorting |
| `pprint` | Pretty-print data structures |
| `reprlib` | Bounded repr for big structures |

**Numbers & math**

| Module | What it does |
|---|---|
| `math` | Floating math functions & constants |
| `cmath` | Complex-number math |
| `decimal` | Exact decimal arithmetic (money!) |
| `fractions` | Exact rational numbers |
| `random` | Pseudo-random numbers (not crypto) |
| `statistics` | Mean, median, stdev, quantiles, correlation |
| `numbers` | Numeric tower ABCs (`Integral`, `Real`) |

**Functional programming**

| Module | What it does |
|---|---|
| `itertools` | Iterator algebra: product, chain, groupby… |
| `functools` | `cache`, `partial`, `reduce`, `wraps` |
| `operator` | Function forms of operators (`itemgetter`, `attrgetter`) |

**Concurrency & parallelism**

| Module | What it does |
|---|---|
| `asyncio` | The async event-loop framework |
| `threading` | Threads, locks, events |
| `multiprocessing` | Processes, pools, queues (true parallelism) |
| `multiprocessing.shared_memory` | Zero-cross-process shared buffers |
| `concurrent.futures` | `ThreadPoolExecutor`/`ProcessPoolExecutor` |
| `subprocess` | Run external programs |
| `queue` | Thread-safe queues (`Queue`, `LifoQueue`, `PriorityQueue`) |
| `sched` | Delayed event scheduler |
| `contextvars` | Context-local state (async-safe “globals”) |
| `signal` | POSIX signal handlers |
| `select` | Wait on streams (select/epoll/kqueue) |
| `selectors` | High-level `select` abstraction |

**File system & I/O**

| Module | What it does |
|---|---|
| `pathlib` | Object-oriented paths (§20) |
| `os` | OS interface: environ, process, walk |
| `os.path` | Legacy path utilities |
| `io` | Streams: `StringIO`, `BytesIO`, buffers |
| `shutil` | High-level file ops: copytree, rmtree, which |
| `tempfile` | Temporary files/directories |
| `glob` | Wildcard path matching |
| `fnmatch` | Unix-style pattern matching on names |
| `fileinput` | Iterate over lines of many files/stdin |
| `linecache` | Random access to file lines (tracebacks use it) |
| `filecmp` | File/directory comparison |
| `getpass` | Password prompts without echo |

**Persistence & databases**

| Module | What it does |
|---|---|
| `pickle` | Object serialization (⚠ untrusted data) |
| `copyreg` | Register pickle support for types |
| `shelve` | Persistent dict of pickled objects |
| `marshal` | Fast internal serialization (bytecode) |
| `dbm` | Simple key-value DBs (`dbm.sqlite` 3.13) |
| `sqlite3` | Embedded SQL database (§20) |
| `plistlib` | Apple property lists |

**Compression & archives**

| Module | What it does |
|---|---|
| `zlib` | Raw DEFLATE compression |
| `gzip` | gzip files/streams |
| `bz2` / `lzma` | bzip2 / xz (LZMA) |
| `zipfile` | Zip archives (also creator of `.whl`) |
| `tarfile` | tar archives |

**Structured data & config formats**

| Module | What it does |
|---|---|
| `json` | JSON encode/decode |
| `csv` | CSV/TSV reading & writing |
| `configparser` | INI files |
| `tomllib` (3.11+) | Parse TOML (pyproject files) |
| `netrc` | `.netrc` login files |
| `email` | MIME message building/parsing (package) |
| `mailbox` | mbox/MH mail folder access |
| `mimetypes` | Filename ↔ MIME type mapping |

**Markup & internet data**

| Module | What it does |
|---|---|
| `html` / `html.parser` / `html.entities` | HTML escape/parse |
| `xml.etree.ElementTree` | The sane XML API |
| `xml.dom` / `xml.dom.minidom` / `xml.dom.pulldom` | DOM APIs |
| `xml.sax` | SAX (streaming) parsing |
| `xml.parsers.expat` | Expat parser bindings |
| `base64` | Base16/32/64 encoding |
| `quopri` | Quoted-printable encoding |
| `urllib.parse` | URL splitting/joining/encoding |

**Networking**

| Module | What it does |
|---|---|
| `socket` | BSD sockets (TCP/UDP/Unix) |
| `ssl` | TLS/SSL wrapping |
| `socketserver` | TCP/UDP server skeletons |
| `ipaddress` | IPv4/IPv6 address & network math |
| `uuid` | UUID generation (1/3/4/5) |
| `mmap` | Memory-mapped files |

**Internet protocols (clients & servers)**

| Module | What it does |
|---|---|
| `urllib.request` / `urllib.error` / `urllib.robotparser` | URL fetching (stdlib HTTP) |
| `http.client` | Low-level HTTP client |
| `http.server` | The quick dev web server |
| `http.cookies` / `http.cookiejar` | Cookie handling |
| `ftplib` | FTP client |
| `imaplib` | IMAP mail client |
| `poplib` | POP3 mail client |
| `smtplib` | SMTP sending |
| `nntplib` † | Usenet — removed in 3.13 |
| `telnetlib` † | Telnet — removed in 3.13 |
| `xmlrpc.client` / `xmlrpc.server` | XML-RPC |
| `webbrowser` | Open the user's browser |
| `wsgiref` | WSGI server/utilities |

**Crypto & hashing**

| Module | What it does |
|---|---|
| `hashlib` | SHA-2/3, blake2, MD5 digests |
| `hmac` | Keyed message authentication |
| `secrets` | Crypto-safe tokens/random |

**OS, platform & environment**

| Module | What it does |
|---|---|
| `time` | Clock reading, sleeping, formatting |
| `argparse` / `getopt` | CLI parsing (§22) |
| `logging` (+ `.config`, `.handlers`) | Logging framework (§22) |
| `gettext` / `locale` | Internationalization |
| `platform` | OS/machine/Python detection |
| `errno` | System error-code constants |
| `ctypes` | Call C shared libraries |
| `curses` | Terminal UIs (Unix; `windows-curses` on Win) |
| `msvcrt` / `winreg` | Windows: MSVC runtime, registry |
| `pwd` / `grp` / `termios` / `tty` / `pty` / `resource` / `syslog` / `posix` | Unix-only system interfaces |

**Multimedia**

| Module | What it does |
|---|---|
| `wave` | WAV file read/write |
| `colorsys` | RGB ↔ HLS/HSV conversion |
| *(removed 3.13)* `audioop`, `aifc`, `sunau`, `chunk`, `imghdr`, `sndhdr` | Legacy audio/image helpers — now third-party |

**GUI & simple frameworks**

| Module | What it does |
|---|---|
| `tkinter` (+ `ttk`, `scrolledtext`) | Standard GUI toolkit (Tcl/Tk) |
| `turtle` | Turtle graphics (learning) |
| `cmd` | Line-oriented command interpreters |
| `shlex` | Shell-like lexing/quoting |

**Development, testing & debugging**

| Module | What it does |
|---|---|
| `typing` | Type hints: `Optional`, `Literal`, `Protocol`… |
| `doctest` | Tests embedded in docstrings |
| `unittest` (+ `unittest.mock`) | xUnit test framework (§7) |
| `pydoc` | Doc extraction (`python -m pydoc`) |
| `pdb` / `bdb` | Debugger engine & builder base (§9) |
| `faulthandler` | Tracebacks on hard crashes |
| `timeit` | Micro-benchmarks |
| `trace` | Execution tracing |
| `tracemalloc` | Memory-allocation tracing |
| `code` / `codeop` | Embedded interactive interpreters |

**Import system & language services**

| Module | What it does |
|---|---|
| `importlib` (+ `.resources`, `.metadata`) | Programmatic imports, data files, dist info |
| `zipimport` | Import from zip archives |
| `modulefinder` | Find modules a script imports |
| `ast` | Parse/transform Python source trees |
| `symtable` | Symbol tables from the compiler |
| `token` / `keyword` / `tokenize` | Language tokens & keywords |
| `tabnanny` | Ambiguous-indentation checker |
| `pyclbr` | Class/function browser info |
| `py_compile` / `compileall` | Bytecode compilation |
| `dis` | Disassembler |

**Removed-in-3.13 watchlist** (you'll still meet these in old code): `aifc` `audioop` `cgi` `cgitb` `chunk` `crypt` `imghdr` `mailcap` `msilib` `nis` `nntplib` `ossaudiodev` `pipes` `sndhdr` `spwd` `sunau` `telnetlib` `uu` `xdrlib` `lib2to3` — plus `formatter`/`parser` (gone in 3.10) and `asyncore`/`asynchat` (gone in 3.12).

### H.2 Essential Third-Party Libraries by Domain

**Web frameworks & APIs**

| Library | What it does |
|---|---|
| `django` | The batteries-included web framework (ORM, admin, auth) |
| `flask` | Micro-framework — you choose the pieces |
| `fastapi` | Modern async APIs with automatic OpenAPI docs |
| `starlette` | The ASGI toolkit under FastAPI |
| `litestar` | Fast, typed, async framework (FastAPI rival) |
| `sanic` / `tornado` | High-performance async frameworks |
| `bottle` / `pyramid` | Minimal / mature mid-size options |
| `jinja2` | The template engine (used by Flask & Ansible) |
| `uvicorn` / `gunicorn` / `hypercorn` | ASGI / WSGI production servers |
| `strawberry-graphql` / `graphene` | GraphQL APIs |

**HTTP & network clients**

| Library | What it does |
|---|---|
| `requests` | The human HTTP client — de-facto standard |
| `httpx` | requests-compatible + async + HTTP/2 |
| `aiohttp` | Async HTTP client & server |
| `urllib3` | Power underneath requests |
| `websockets` / `websocket-client` | Async / sync WebSocket |
| `pysocks` / `python-socks` | SOCKS proxies |

**Web scraping & parsing**

| Library | What it does |
|---|---|
| `beautifulsoup4` | Tolerant HTML parsing & extraction |
| `lxml` | Fast C XML/HTML (XPath, XSLT) |
| `scrapy` | Full crawling/spider framework |
| `selectolax` / `parsel` | Very fast HTML parsers / XPath+CSS selectors |

**Databases & ORMs**

| Library | What it does |
|---|---|
| `sqlalchemy` | The SQL toolkit & ORM — industry standard |
| `peewee` / `pony` / `tortoise-orm` | Small sync ORMs / async ORM |
| `alembic` | Schema migrations for SQLAlchemy |
| `psycopg` (v3) / `psycopg2-binary` | PostgreSQL drivers |
| `pymysql` / `mysql-connector-python` / `mariadb` | MySQL/MariaDB drivers |
| `pymongo` / `motor` | MongoDB sync / async |
| `redis` / `hiredis` | Redis client + C parser |
| `elasticsearch` | Elasticsearch client |
| `influxdb-client` | Time-series DB client |
| `cassandra-driver` / `neo4j` | Wide-column / graph DB drivers |

**Data analysis & dataframes**

| Library | What it does |
|---|---|
| `numpy` | N-dim arrays — foundation of all science in Python |
| `pandas` | DataFrames: wrangle, join, aggregate tabular data |
| `polars` | Rust-powered DataFrames, much faster than pandas |
| `pyarrow` | Columnar Arrow memory/format (parquet, interop) |
| `dask` / `modin` | Parallel/out-of-core pandas scaling |
| `great-expectations` / `pandera` | Data validation |

**Visualization**

| Library | What it does |
|---|---|
| `matplotlib` | The plotting foundation |
| `seaborn` | Statistical charts on matplotlib |
| `plotly` | Interactive charts & dashboards |
| `bokeh` | Interactive browser visualizations |
| `altair` | Declarative statistical graphics |
| `folium` | Leaflet maps |

**Machine learning & statistics**

| Library | What it does |
|---|---|
| `scikit-learn` | Classical ML: regression, trees, clustering, pipelines |
| `xgboost` / `lightgbm` / `catboost` | Gradient-boosting champions |
| `statsmodels` | Classical statistics & econometrics |
| `optuna` | Hyperparameter optimization |
| `imbalanced-learn` | Resampling for skewed classes |

**Deep learning & AI**

| Library | What it does |
|---|---|
| `torch` (PyTorch) | Research-favorite deep-learning framework |
| `tensorflow` / `keras` | Production DL stack |
| `jax` / `flax` | Composable autodiff on GPU/TPU |
| `transformers` (HF) | Pretrained models — NLP and beyond |
| `diffusers` | Stable-diffusion image generation |
| `ultralytics` | YOLO object detection |
| `openai` / `anthropic` / `google-genai` | LLM provider SDKs |
| `langchain` / `llama-index` | LLM application frameworks |
| `sentence-transformers` | Embeddings & semantic search |
| `whisper` (openai-whisper) | Speech-to-text |
| `onnx` / `onnxruntime` | Model interchange & inference |
| `mlflow` / `wandb` / `ray` | Experiment tracking / distributed compute |

**Computer vision & images**

| Library | What it does |
|---|---|
| `opencv-python` | The CV swiss army knife |
| `pillow` | Image read/write/resize (PIL fork) |
| `scikit-image` | CV algorithms on numpy arrays |
| `imageio` / `imgaug` / `albumentations` | IO for all formats / training augmentations |
| `easyocr` / `paddleocr` | OCR engines |
| `cairosvg` / `wand` | SVG→PNG / ImageMagick bindings |

**Audio, video & multimedia**

| Library | What it does |
|---|---|
| `pydub` | Easy audio cutting/conversion |
| `librosa` | Music & audio analysis |
| `soundfile` / `pyaudio` | Read-write sound / record & play |
| `speechrecognition` | STT front-ends |
| `moviepy` / `ffmpeg-python` | Video editing / ffmpeg bindings |

**GUI & desktop apps**

| Library | What it does |
|---|---|
| `pyside6` / `pyqt6` | Qt applications (official / commercial-ish) |
| `kivy` | Natural UIs, touch, mobile |
| `wxpython` | Native-widget toolkit |
| `customtkinter` | Modern-looking tkinter |
| `dearpygui` | GPU-rendered immediate-mode GUI |
| `flet` / `nicegui` | Flutter-style / web-tech UIs in Python |
| `pystray` / `pywin32` | Tray icons / full Windows API |

**Games**

| Library | What it does |
|---|---|
| `pygame` / `pygame-ce` | The classic 2D game engine (CE = community fork) |
| `arcade` | Modern 2D, OpenGL |
| `panda3d` / `ursina` | 3D engine / cute 3D wrapper |
| `renpy` | Visual novels |

**CLI & terminal UX**

| Library | What it does |
|---|---|
| `typer` / `click` | Type-hint / decorator CLI builders |
| `rich` | Rich text, tables, progress in terminal |
| `textual` | Full TUI apps (by the rich author) |
| `prompt-toolkit` / `questionary` / `inquirer` | Interactive prompts |
| `tqdm` / `alive-progress` | Progress bars for loops |
| `colorama` / `blessed` | Cross-platform colors / terminal control |

**Testing & quality**

| Library | What it does |
|---|---|
| `pytest` (+ `pytest-cov`, `pytest-xdist`, `pytest-mock`, `pytest-asyncio`) | Testing framework & plugins |
| `hypothesis` | Property-based testing |
| `tox` / `nox` | Matrix test automation |
| `faker` / `factory-boy` | Fake data / object factories |
| `selenium` / `playwright` | Browser automation & E2E |
| `locust` | Load testing |
| `robotframework` | Keyword-driven acceptance testing |
| `coverage` | Line/branch coverage |

**Linting, formatting & typing**

| Library | What it does |
|---|---|
| `ruff` ⭐ | Linter+formatter, Rust-fast (replaces many below) |
| `black` / `isort` | Formatter / import sorter |
| `mypy` / `pyright` | Static type checkers |
| `pylint` / `flake8` / `pydocstyle` | Classic linters / docstring style |
| `bandit` / `semgrep` | Security scanners |
| `pre-commit` | Git hook manager |
| `pylint-django` etc. | Framework-aware plugins |

**Packaging, build & environments**

| Library | What it does |
|---|---|
| `pip` / `setuptools` / `wheel` | The install/build base |
| `build` / `twine` | Build sdist+wheel / upload to PyPI |
| `poetry` / `pdm` / `hatch` | Project managers |
| `uv` ⭐ | Blazing-fast everything (pip/venv/pipx/python) |
| `pipx` | Install CLI apps isolated |
| `pipenv` / `virtualenv` | Legacy env managers |
| `pyinstaller` / `nuitka` / `cx-freeze` | Freeze to standalone executables |
| `shiv` / `pex` | Zipapps — single-file executables |
| `conda` / `mamba` | Science-oriented env/package managers |

**Task queues, scheduling & workflow**

| Library | What it does |
|---|---|
| `celery` | Distributed task queue standard |
| `rq` / `dramatiq` / `huey` | Lighter task queues |
| `apscheduler` | In-process job scheduling |
| `airflow` / `prefect` / `dagster` | Data-pipeline orchestrators |
| `kafka-python` / `confluent-kafka` | Kafka clients |
| `pika` | RabbitMQ (AMQP) |
| `pyzmq` | ZeroMQ messaging |
| `nats-py` | NATS messaging |

**Serialization, validation & settings**

| Library | What it does |
|---|---|
| `pydantic` (v2) | Data validation via type hints (FastAPI's core) |
| `attrs` / `cattrs` | Class builder without inheritance |
| `marshmallow` | Schema serialization |
| `orjson` / `ujson` | Ultra-fast JSON |
| `msgspec` ⭐ | Fast JSON/msgpack + validation |
| `protobuf` / `flatbuffers` / `thrift` | Binary schema formats |
| `python-dotenv` / `pydantic-settings` / `dynaconf` | Env/config loading |
| `hydra-core` / `omegaconf` | Hierarchical experiment configs |

**Office documents & PDFs**

| Library | What it does |
|---|---|
| `openpyxl` / `xlsxwriter` | Excel xlsx read-write / fast writing |
| `python-docx` / `python-pptx` | Word / PowerPoint editing |
| `pypdf` / `pdfplumber` | PDF merge/split / text+table extraction |
| `reportlab` / `fpdf2` / `weasyprint` | PDF generation (programmatic / HTML→PDF) |
| `camelot` / `tabula-py` | Table extraction from PDFs |
| `python-docx-template` / `docxtpl` | Jinja2 templates for Word |
| `pandoc` (`pypandoc`) | Universal document conversion |

**Date, time & utilities**

| Library | What it does |
|---|---|
| `python-dateutil` | Parser (`parse("3 days ago"…)`), rrule |
| `pendulum` / `arrow` | Nicer datetime libraries |
| `pytz` | Legacy tz database (use `zoneinfo` now) |
| `freezegun` / `time-machine` | Freeze time in tests |
| `humanize` / `prettytable` / `tabulate` | Human strings / ASCII tables |
| `more-itertools` / `toolz` | Even more iterator/functional helpers |
| `cytoolz` | C-accelerated toolz |

**System, environment & observability**

| Library | What it does |
|---|---|
| `psutil` | Processes, CPU, memory, disks, network |
| `watchdog` | Cross-platform filesystem events |
| `pyperclip` | Clipboard access |
| `send2trash` | Safe delete-to-recycle-bin |
| `diskcache` / `cachetools` / `aiocache` | Persistent / in-proc / async caches |
| `loguru` / `structlog` | Painless / structured logging |
| `sentry-sdk` / `opentelemetry` | Crash reporting / tracing |

**Security & crypto**

| Library | What it does |
|---|---|
| `cryptography` | The modern crypto library (TLS, X.509, AEAD) |
| `pyjwt` / `python-jose` | JWT encode/verify |
| `passlib` / `argon2-cffi` / `bcrypt` | Password hashing |
| `authlib` | OAuth1/2, OIDC |
| `paramiko` / `fabric` / `netmiko` | SSH / SSH automation / network devices |
| `scapy` | Packet crafting & sniffing |
| `impacket` / `pwntools` | Windows protocols CTF/pentest toolkit |
| `certifi` | The CA certificate bundle trusted by requests/httpx |

**Science & engineering**

| Library | What it does |
|---|---|
| `scipy` | Optimization, signal, linear algebra, stats |
| `sympy` | Symbolic math (CAS) |
| `numba` / `cython` | JIT / compile Python to C speed |
| `networkx` | Graph algorithms |
| `pint` / `uncertainties` | Units / error propagation |
| `astropy` | Astronomy |
| `biopython` | Bioinformatics |
| `qutip` | Quantum physics |
| `geopandas` / `shapely` / `rasterio` | Geospatial dataframes / geometry / rasters |

**Docs, notebooks & education**

| Library | What it does |
|---|---|
| `jupyterlab` / `notebook` / `ipython` | Interactive computing |
| `ipywidgets` / `papermill` | Widget UIs / parameterized notebooks |
| `sphinx` / `mkdocs-material` | Doc site generators |
| `mkdocstrings` / `autodoc` | API docs from docstrings |
| `pdoc` | Zero-config API docs |

### H.3 How to choose a library (30-second method)

1. `pip index versions name` — is it alive? Last release recent?
2. Check PyPI page: does it support your Python version? Wheel available (no compiler needed)?
3. Gut-check health: maintained repo, issues answered, tests, license permissive (MIT/BSD/Apache)?
4. Any heavyweight deps it drags in? (`pip install --dry-run`)
5. Search “alternatives to X” — the ecosystem moves (requests→httpx, pandas→polars, pip→uv).
6. For anything security-sensitive: is it widely audited (`cryptography`, not random forks)?

Every package above is installable with `pip install name` / `uv pip install name` (§3–§4) — and browsable at `pypi.org/project/<name>` with docs, changelog and dependency info.

---

## Keep Learning

- Official tutorial & library reference: **docs.python.org/3** (the single best free resource)
- Practice: **exercism.org/tracks/python**, **adventofcode.com**, project ideas → build, don't just read
- Real-world code reading: browse the stdlib source (`Lib/` in the CPython repo) — it's readable Python!
- 7-day path with this doc: Day 1 §0–1 · Day 2 §11–14 · Day 3 §15–17 · Day 4 §18–19 · Day 5 §20 · Day 6 §21–22 · Day 7 T1–T10 of your choice
- When stuck: read the traceback bottom-up → `help()`/`dir()` → docs.python.org → search the exact error line

*End of reference — 70 built-ins, 40+ tool subcommand tables, complete language core, 10 tutorials, complete library catalog. Happy hissing.* 🐍
