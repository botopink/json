# json

> Repository: `botopink/json` (`git@github.com:botopink/json.git`) · in the meta checkout: `repository/json/`

The JSON value type and its codec (decision 396): the `Json` type and its methods, `parse`, `decode`, `stringify`, `quote` — moved whole from std's `json.bp` by 142 step 1; std knows nothing of JSON.

A library of its own (decision 396, decision 326's rule). It is filled by
`specs/1.0.12-beta/03-bundled-libs/142-data-formats`; until its step lands this repository holds
only its scaffold.

## Hooks

Every clone runs the shared pre-commit gate:

```sh
git config core.hooksPath scripts/git-hooks
```

`scripts/git-hooks/pre-commit` and `scripts/git-hooks/lib/runner-standalone.sh` are byte-identical
across the library repositories (the meta repository's CI check 4); edit them in one place and copy.
