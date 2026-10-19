# Decision 778 — json's helpers (396 (1)): `unquote(s: string) -> Result<string, JsonError>` reads a JSON string literal back to its text, the inverse of `quote`; `array(items: string[]) -> string` and `object(members: #(string, string)[]) -> string` join texts that are already JSON values into one JSON text, no escaping of the parts.

The program writes one JSON text with json's helpers and reads a string literal back. `quote("say \"hi\"")` is the literal with its quotes and the inner quotes escaped, and `unquote` of that literal answers the text again, `say "hi"`: the two are inverses. `unquote` of something that is not a JSON string literal — the number `42`, a bare word — answers an `Error` carrying a `JsonError`, here turned into `refused` by `catch`. `array` and `object` escape nothing: each item and each member's value is already a JSON value (a `quote` output, a number's text, `true`), and they only join them, so the program prints `{"name":"Ada","tags":["math","code"],"born":1815,"active":true}`. A part that is not a JSON value — the bare `Ada` passed as a value — is the caller's error, not checked: `object` joins it as it is, and `decode` of the result is the place where it fails, which is why the last line prints `true false`.

Departure: the json repository holds no `src/` yet (144 B-27, 151 s1 move std's `json.bp` here), so the import of `"json"` resolves nothing and the example does not build; std's `json.unquote` answers `Result<string, HostError>` today, not `JsonError`.

Cells in this repository that prove it: none yet — json holds no cell beside its decision cells.

[draft/main.bp](draft/main.bp)
