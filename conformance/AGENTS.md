# conformance

The `json` library's conformance tree; [`docs.md`](docs.md) is its reference. The library holds no `src/` yet, so each section of the reference is marked as decided and not yet built, and is rewritten from the declarations when 144 B-27 and 151 s1 land.

- `docs.md` — the reference: `Json` and its numbers (396, 332, 500), `decode` and `encode` (336), the text helpers, the consumers and the departures from the spelling in force.
- `modules/decisions-taken/<slug>-<N>/` — the decision cells (front 166, decisions 646–651): one per code-bearing row of
  the generated `../decisions-taken.md`, each a `docs.md` (its first line generated) and its example, `draft/main.bp`
  (the `////` header generated) until 166 s4 promotes it to `src/` with a `botopink.json`. Kept by
  `scripts/decision-cells.py` of the meta repository (`scaffold`, `compile`, `check` — meta CI check 7); the subtree
  is front 166's alone (651).
