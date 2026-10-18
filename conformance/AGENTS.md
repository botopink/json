# conformance

The `json` library's conformance tree; [`docs.md`](docs.md) is its reference.

- `modules/decisions-taken/<slug>-<N>/` — the decision cells (front 166, decisions 646–651): one per code-bearing row of
  the generated `../decisions-taken.md`, each a `docs.md` (its first line generated) and its example, `draft/main.bp`
  (the `////` header generated) until 166 s4 promotes it to `src/` with a `botopink.json`. Kept by
  `scripts/decision-cells.py` of the meta repository (`scaffold`, `compile`, `check` — meta CI check 7); the subtree
  is front 166's alone (651).
