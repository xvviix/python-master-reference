# 🐍 Python Master Reference

**Every CLI tool & subcommand · the complete language · standard library · 10 hands-on tutorials · 7 appendices**

🌐 **[View the online edition →](https://xvviix.github.io/python-master-reference/)**

A complete, offline-capable Python 3 reference covering:

| Part | Contents |
|---|---|
| **Part 0** | Getting started — versions, install, running Python 7 ways, REPL/IPython, virtualenvs & the packaging zoo |
| **Part 1** | The command line — `python` (every flag), `py`, `pip` (every subcommand), `venv`/`pipx`/`poetry`/`conda`/`uv`, `python -m` toolbox, packaging & publishing, `pytest`/`unittest`/coverage, ruff/black/mypy, `pdb` & profiling, Jupyter |
| **Part 2** | The language — every built-in type & method, operators & precedence, f-strings & regex, control flow & comprehensions, `itertools`/`functools`, functions & typing, OOP & dataclasses, full exception hierarchy, imports, files & `pathlib`, concurrency (threads/async), stdlib essentials (`datetime`, `argparse`, `logging` full walkthroughs) |
| **Part 3** | Tutorials T1–T10 — first hour, log parsing, REST APIs, CLI apps, dataclass OOP, publish to PyPI, pytest, automation, asyncio, debugging & profiling |
| **Part 4** | Appendices A–H — tool index, all 70 built-ins, dunder protocol, format specs, real-world exceptions, one-liners, best practices, **complete library catalog** (full standard library + ~250 essential third-party libraries by domain) |

## Install the libraries

The repo ships ready-made requirements files (all verified on a clean Python 3.13 venv):

```bash
python -m venv .venv && source .venv/bin/activate   # Windows: .venv\Scripts\activate
python -m pip install -r requirements.txt            # core: requests, httpx, pydantic, numpy, pandas, matplotlib, rich, typer…
python -m pip install -r requirements-dev.txt        # dev: pytest, ruff, mypy, hypothesis, pre-commit…
# need more? uncomment a group in requirements-domains.txt (web, ML, GUI, security, science…)
```

| File | Contents |
|---|---|
| `requirements.txt` | 19 core runtime libraries, version-floored to current releases |
| `requirements-dev.txt` | 8 development & quality tools |
| `requirements-domains.txt` | ~90 libraries in commented domain groups — uncomment what you need |

## Files

| File | Description |
|---|---|
| [`index.html`](index.html) | Single-file interactive site — search, sidebar nav, dark mode, copy buttons |
| [`Python_Master_Reference.md`](Python_Master_Reference.md) | Markdown source (~2,000 lines) |
| [`Python_Master_Reference.html`](Python_Master_Reference.html) | Same site under its full name |

## Features (HTML edition)

🔍 live section search · 🧭 sidebar with scroll-spy · 📋 copy buttons on every code block · 🌙 dark/light theme · 📱 responsive · 🖨️ print-friendly — one self-contained file, zero external dependencies.

---
*Generated as a study/reference document. Contributions welcome via issues/PRs.*
