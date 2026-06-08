---
MEP: XXXX
Title: Notebook Naming Convention
Discussion: XXX
Implementation: N/A
---

# Notebook Naming Convention

## Abstract

This MEP proposes `_mo.py` as a standard naming convention for marimo
notebooks. This convention distinguishes marimo notebooks from regular Python
files while maintaining full compatibility as Python modules, enabling better
tooling integration without introducing new file extensions.

## Motivation

MEP-0001 establishes that marimo notebooks are stored as pure Python files. As
the marimo ecosystem grows, the goal is to identify a way of marking marimo
files such that they can be easily identified as marimo notebooks. Currently
this requires inspecting the file contents.

One approach is to introduce a new file extension. For example, Jupyter
notebooks use `.ipynb` for JSON files. Some suggestions for marimo have been
`.mo.py` or `.mpy`. These are unambiguous but are strict and break several
benefits of MEP-0001: automatic syntax highlighting, Python's import system,
and module compatibility. It would take considerable time to build ecosystem
support and require special tooling configuration.

A more pragmatic approach is to standardize around an optional naming
convention. This allows easy identification and organization of notebooks while
preserving the "just Python" philosophy of marimo. The Python ecosystem has
precedent for such conventions: `test_*.py` for pytest files, `_*.py` for
private modules.

## Specification

The keywords in this document are to be interpreted as described in [RFC
2119](https://datatracker.ietf.org/doc/html/rfc2119).

### Naming Convention

- Marimo notebook files SHOULD use the suffix `_mo.py`
- Examples: `analysis_mo.py`, `dashboard_mo.py`, `tutorial_mo.py`
- Tools MAY recognize `_mo.py` files as marimo notebooks for specialized handling
- Marimo itself SHALL NOT require this naming convention for notebook functionality

This is purely a community convention with no special behavior required in marimo
itself. Adopting this convention enables:

- Simple pattern matching with glob patterns (`*_mo.py`)
- Editor extensions to provide marimo-specific features
- Clear visual distinction in file explorers
- Build tools to identify notebooks for special processing

## Evaluation

The `_mo.py` convention satisfies key requirements:

- **Python compatibility**: Full import and tooling support maintained
- **Editor support**: Syntax highlighting and language features work normally
- **Simple detection**: Suffix-based matching is straightforward
- **Version control**: No impact on git diff readability
- **Pythonic**: Follows established Python naming patterns
- **Non-breaking**: Requires no changes to marimo or Python

## Alternatives Considered

1. **`.mpy` extension** - Would break editor syntax highlighting and IDE
   support. The `.mpy` extension is also already used for MicroPython compiled
   files.

2. **`.mo.py` double extension** - Breaks Python's import system which expects
   single `.py` extension. Would prevent notebooks from being imported as
   modules.

3. **`mo_*.py` prefix** - Less conventional in Python ecosystem and prevents
   simple suffix-based file matching that most tools prefer.

4. **No convention** - Maintains status quo but misses opportunity for
   ecosystem tooling improvements.

## Future Considerations

While this MEP proposes only a naming convention, future marimo versions or
tools MAY choose to recognize `_mo.py` files for enhanced features such as:

- Specialized linting rules
- Custom file icons in IDEs
- Quick-open commands in editors
- Build tool integrations

These features SHALL remain fully optional and backward compatible, as `_mo.py`
files remain standard Python modules.
