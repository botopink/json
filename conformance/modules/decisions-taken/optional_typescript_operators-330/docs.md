# Decision 330 — `?T` is read with TypeScript's operators and has no methods; `result` goes; a type declared in a type is its associated type.

The program reads a decoded document only through the operators of `?T`. `Json.field` answers `?Json`: `doc.field("name")?.str() ?? "anonymous"` reads a present member, the same chain on `"version"` falls back to `"0.0.0"`, and `?.items()` on `"tags"` answers `?Json[]`, flattened rather than nested, before `??` gives `[]`. `tags.at(0)?.str()` chains once more on the optional the array answers. The `??` beside `||` sits in parentheses, the one way the two may meet, and `doc.field("tags")!` asserts presence, checked when the program runs. No `?T` method is called: `isError()` and `unwrapOr` appear only on the `Result` that `decode` answers, as methods, with no `result` namespace. `Origin` is declared inside `Settings`, so it is `Settings`'s associated type, written `Settings.Origin` both in `read`'s signature and at its construction. The program prints the path, the name, the fallback version, the first tag, `true` and `an array`.

Cells in this repository that prove it: none yet — `json` holds no code and no cell beside its decision cells until 144 B-27 and 151 s1 move std's `json.bp` here.

[draft/main.bp](draft/main.bp)
