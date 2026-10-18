# Decision 396 — Markdown, YAML and JSON are three libraries of their own — `markdown`, `yaml`, `json` (`botopink/{markdown,yaml,json}` at `repository/{markdown,yaml,json}`, 326's rule) — and std knows nothing of JSON.

The program is a consumer of the `json` library: everything it does with JSON comes from `from "json"` — the `Json` value and its readers `field`, `items`, `str` and `isObject`, and the functions `decode`, `encode`, `quote`, `unquote`, `array` and `object` — while from std it imports only the terminal. It writes a document with `object`, `array` and `quote`, reads it back with `decode`, takes the formats' texts and round-trips the name through `quote` and `unquote`, then prints `true`, `botopink`, `json yaml markdown` and the document as `encode` writes it. A consumer package declares `json` as a dependency in its manifest; nothing of std names JSON, so the import from `"json"` is the only way the program reaches any of it.

Cells in this repository that prove it: none yet — `json` holds no code and no cell beside its decision cells until 144 B-27 and 151 s1 move std's `json.bp` here.

[draft/main.bp](draft/main.bp)
