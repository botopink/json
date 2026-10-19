# Decision 337 — The shorthand import goes; `mod m;` binds the namespace `m` in the module that declares it.

The program prints the title and the page count of one decoded document. `readers/fields.bp` is a module of the package, `readers.fields`, its path its name, and declares `title` and `pageCount` as `pub`. `main.bp` imports both by that path in braces with no `from`: `import {readers.fields.title, readers.fields.pageCount};`, the module first and then the item. Every other name arrives by an import that names its source: `io.terminal` `from "std"`, `Json` and `decode` `from "json"`.

The refused spelling is the shorthand. `import {title};` has no `from`, and its first segment names no module of the package, so it is refused with `shorthand-import` at the item, the fix written: `import {readers.fields.title};`, the line the example uses. A bare `import {decode};` does not reach the library either; it is written `from "json"`.

337 (2)'s `mod m;` namespace is replaced by decision 592 (1): every `.bp` under `src/` is a module, there is no `mod` / `pub mod`; and with 337 (3) there is no combined form and no re-export syntax, so a name has the one path of the module that declares it.

Cells in this repository that prove it: none yet — `json` holds no code and no cell beside its decision cells until 144 B-27 and 151 s1 move std's `json.bp` here.

[draft/main.bp](draft/main.bp)
[draft/readers/fields.bp](draft/readers/fields.bp)
