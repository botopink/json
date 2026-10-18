# Decision 500 — `json` leaves std first (142 s1); `Json`'s numbers land in the json repository, `Decimal` stays in std.

The program decodes `[42, 12345678901234567890, 1.50]` with the `json` library and walks the three numbers. `describe`'s `case` has no `Num` arm: the integer within `i64` is `Int`, the larger one `BigInt`, the numeral with a fraction `Dec`, so it prints `i64 42; bigint 12345678901234567890; decimal 1.50`. `i64()` answers `42` for the first item and `null` (here `-1` through `??`) for the decimal, never a coercion. `exact` answers the third item as a std `Decimal`, imported `from "std"` beside `Json` `from "json"`: the number type lives in the json library, the exact decimal stays in std, and its scale is kept, `1.50`. `isIntegral()` is `true` for the big integer, and `encode` writes the array back with each number exact.

Cells in this repository that prove it: none yet — `json` holds no code and no cell beside its decision cells until 144 B-27 and 151 s1 move std's `json.bp` here.

[draft/main.bp](draft/main.bp)
