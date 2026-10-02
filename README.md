# Orangeplsda — PLS-DA & OPLS-DA for Orange3

Custom Orange3 add-on providing **PLS-DA** (Partial Least Squares
Discriminant Analysis) and **OPLS-DA** (Orthogonal PLS-DA, Trygg & Wold 2002)
classification widgets, plus S-Plot support for biomarker discovery.

## Widgets

- **PLS-DA** — classification learner wrapping sklearn `PLSRegression` (one-hot Y)
- **OPLS-DA** — separates predictive from orthogonal variation

Both appear in Orange under the **PLS-DA** category, next to the built-in PLS-R.

## Installation (any Orange3 ≥ 3.40)

Use **Orange's own Python**, not `/usr/bin/python3`.

### macOS (Orange.app)

```bash
/Applications/Orange.app/Contents/Frameworks/Python.framework/Versions/Current/bin/python3 -m pip install .
```

### Windows (Orange Command Prompt) / Linux / conda

```bash
python -m pip install .
```

### From GitHub (team workflow)

```bash
python -m pip install git+https://github.com/<org>/orange-plsda-addon.git
```

Widgets appear on the next canvas open — no Orange restart needed.

## Development

```bash
# editable install with Orange's Python
python -m pip install -e .
```

Run the learner smoke tests:

```bash
python -c "
from Orange.data import Table
from Orange.base import Model
from orangeplsda import PLSDALearner
from orangeplsda.oplsda_learner import OPLSDALearner
for L, kw in [(PLSDALearner, dict(n_components=2)),
              (OPLSDALearner, dict(n_components=1, n_ortho=1))]:
    t = Table('iris'); m = L(**kw)(t)
    p, pr = m(t, ret=Model.ValueProbs)
    print(L.__name__, (p == t.Y.flatten()).mean(), pr.shape)
"
```

## License

MIT