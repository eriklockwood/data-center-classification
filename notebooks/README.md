# Notebooks

Exploratory and analysis notebooks live here. Notebooks are for investigation and narrative; reusable code should graduate into `src/data_center_classification/`.

## Naming

`NN-author-topic.ipynb`, where `NN` is a zero-padded sequence number that increments across the project.

Examples:
- `01-erik-osti-eda.ipynb`
- `02-zoe-ejscreen-feature-build.ipynb`
- `03-erik-mce-prototype.ipynb`

## Conventions

- Import the project package — never use `sys.path` hacks or relative path tricks:
  ```python
  import data_center_classification as dcc
  ```
- The package is installed in editable mode via `uv sync`; new files in `src/` are picked up immediately, no reinstall needed.
- Clear cell outputs before committing if outputs are large or contain plotted figures with many points (keeps diffs reviewable).
- If a notebook produces a reusable utility, refactor it into `src/data_center_classification/` and re-import.
