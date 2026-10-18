# Decision 337 — The shorthand import goes; `mod m;` binds the namespace `m` in the module that declares it.

`main.bp` declares `mod readers;` and calls `readers.title(doc)` and `readers.pageCount(doc)` with no import of `readers`: the declaration binds the namespace in the module that writes it. `readers` is a folder module: `readers/mod.bp` declares `mod fields;` privately and exposes the two functions of `readers/fields.bp` as values, `pub val title = fields.title;`, so each name has one public path, `readers.title`, and none through `readers.fields`. Every other name arrives by an import that says where it comes from — `from "std"`, `from "json"`. A bare `import {title};`, a name with no module path and no `from`, is the refused shorthand; its fix is the module path. The program prints the title and the page count of one decoded document.

Cells in this repository that prove it: none yet — `json` holds no code and no cell beside its decision cells until 144 B-27 and 151 s1 move std's `json.bp` here.

[draft/main.bp](draft/main.bp)
[draft/readers/mod.bp](draft/readers/mod.bp)
[draft/readers/fields.bp](draft/readers/fields.bp)
