# Decision 206 — `import {…} from "<name>"` resolves only to a package — std, a bundled package or a declared dependency.

The program imports from two packages and from one of its own modules. `import {io.terminal} from "std"` and `import {Json, decode} from "json"` each name a package after `from`: std, and `json`, the dependency a consumer declares. `report` is a module of the program's own package: every `.bp` file of the package is one of its modules, named by its path, so nothing declares it, and `main.bp` reaches its `summary` by the path in braces, `import {report.summary};`, with no `from`; `report.bp` in turn imports `Json` from the `json` package the same way `main.bp` does. Writing `import {summary} from "report"` would name a module of this package after `from` and is the refused form, whose fix is the brace path the example writes. The program decodes one object and prints its kind and member names through `summary`.

Cells in this repository that prove it: none yet — `json` holds no code and no cell beside its decision cells until 144 B-27 and 151 s1 move std's `json.bp` here.

[draft/main.bp](draft/main.bp)
[draft/report.bp](draft/report.bp)
