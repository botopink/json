# json — conformance

`json` is the JSON value type and its codec: the `Json` type and its methods, `decode`, `encode`, `quote`, `unquote`, `array`
and `object`. It is one of the three data-format libraries (`json`, `yaml`, `markdown`) that are repositories of their own,
and std knows nothing of JSON (decisions 396, 326). Every example is a conformance cell (decisions 461, 463, 465). This
repository holds no `src/` yet: the library's code arrives when std's `json.bp` moves here (144 B-27, 151 s1), so there is
no module to describe from its declarations, and no cell beside the decision cells. This reference therefore states the
library as the decisions fix it, and each section is marked as decided and not yet built. When a module lands, its section
is rewritten from its declarations and the `///` comments there, and the cells that prove it join
[`modules/decisions-taken/`](modules/decisions-taken/) (decision 465, step 5). A table, a grammar or a wire format is not a
program and is fenced as `text`.

| Section | What |
|---|---|
| *Where the library stands* | what the repository holds, and what each decision fixes about it |
| *Json* | the value type, its numbers, its readers |
| *decode and encode* | the one way in and out, strict on both |
| *Text helpers* | `quote`, `unquote`, `array`, `object` |
| *Consumers* | how a program reaches the library |
| *Departures from the spelling in force* | what the scaffold still writes in a retired form |

| Directory | What it holds |
|---|---|
| [`modules/decisions-taken/`](modules/decisions-taken/) | One directory per decision of [`../decisions-taken.md`](../decisions-taken.md) that fixes program behaviour, `<slug>-<N>/` (decisions 646–648): a `docs.md` walking through the decision's one example and naming the cells that prove it, and the example itself, `draft/main.bp` until front 166 s4 promotes it to a cell (649) |

## Where the library stands

The repository holds its scaffold: `botopink.json` (the package `json`, targets `erlang` and `commonJS`), the gate and the
decision cells. [data_formats_are_own_libraries-396](modules/decisions-taken/data_formats_are_own_libraries-396/draft/main.bp)
is the program of a consumer of the library: everything it does with JSON comes from `from "json"`, and from std it imports
only the terminal. The library is pure botopink with no host cell, so it runs at build on the wasm comptime runtime on both
hosts, `wasi` and `browser` (336, 594;
[libraries_run_at_build_on_wasm-594](modules/decisions-taken/libraries_run_at_build_on_wasm-594/draft/main.bp)).
Its own imports follow 206 and 337: a module of the package by its path in braces with no `from`, a package with `from`, and
no bare name
([own_module_import_without_from-206](modules/decisions-taken/own_module_import_without_from-206/draft/main.bp),
[shorthand_import_refused-337](modules/decisions-taken/shorthand_import_refused-337/draft/main.bp)). A `?T` that a reader
answers is read with `??`, `?.` and `!`, never methods
([optional_typescript_operators-330](modules/decisions-taken/optional_typescript_operators-330/draft/main.bp)).

## Json

Decided, not yet built (396 (1), 332 (4), 500). `Json` is the value type std's `json.bp` held, taken whole, with its methods:
`members`, `field`, `str`, `items`, `isObject`, `kindName` and the rest of its readers. It chooses a number by the numeral:

```text
an integer within i64          Int(value: i64)
a larger integer               BigInt(value: bigint)
a fraction or an exponent      Dec(value: Decimal)      exact
```

`Num(value: f64)` goes. The readers `num() -> ?f64`, `i64()`, `bigint()` and `decimal()` answer exactly or `null` when the
value does not fit, never a coercion; `isNumber()` and `isIntegral()` test the kind. Writing keeps the value exact. The type
`Json` lives in this library, and `Decimal` stays in std (500): a program imports `Json` `from "json"` and `Decimal` `from
"std"`. [json_numbers_in_json_library-500](modules/decisions-taken/json_numbers_in_json_library-500/draft/main.bp) decodes
`[42, 12345678901234567890, 1.50]`, walks the three numbers through a `case` with no `Num` arm, and writes them back.

## decode and encode

Decided, not yet built (336, 396). `decode` and `encode` are the one way, on every target and both wasm hosts, and both are
botopink bodies. `json.parse` and `json.stringify` are gone. `decode` is strict and answers a `Result`: a duplicate member,
an overflow and an unpaired surrogate are each an `Error`, and members are kept in document order. `encode` writes in
document order, with numbers exact.

## Text helpers

Decided, not yet built (396 (1)). `quote` writes a string as a JSON string literal, escaping every control character, and
`unquote` is its inverse. `array` and `object` assemble a document from texts that are already JSON — `array` from a list of
element texts, `object` from `#(key, text)` pairs in order — which is how the `actions` envelope and RPC body are written.
The cell [data_formats_are_own_libraries-396](modules/decisions-taken/data_formats_are_own_libraries-396/draft/main.bp)
writes a document with `object`, `array` and `quote`, reads it back with `decode`, round-trips a name through `quote` and
`unquote`, and prints the document as `encode` writes it.

## Consumers

A consumer declares the dependency in its `dependencies` (242) and imports `from "json"`: rakun, validation, rakun-ssr,
rakun-bpp, actions and log (396 (1)). `yaml` reads one YAML subset into `Json`, and `markdown` answers a tree of its own;
neither is part of this library.

## Departures from the spelling in force

- `botopink.json`'s description still names `parse` and `stringify`, which are gone (336); the library's functions are
  `decode` and `encode`.
