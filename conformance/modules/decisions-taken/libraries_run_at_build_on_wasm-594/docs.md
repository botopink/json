# Decision 594 — Every library runs at build on the wasm comptime runtime (434), jhonstart first; a function only Erlang or Node can run is a located error there.

Both values the program prints are computed with `comptime`, so they run at build on the wasm comptime runtime whatever target the program is built for. `object` and `quote` come from the `json` library, and `quote`'s host cells carry a wasm form, so `manifest` is one text — the tab escaped as `\t` — on every target. `label` is a host cell of the program itself: its Erlang and JavaScript templates serve the run-time targets and `.Wasm(body: labelBody)` gives it the botopink body the build runs, so `comptime label(quote("name"))` answers `key:"name"`. Had `label` carried only `.Erlang` and `.JavaScript`, the `comptime` call would be refused at build, at the call, naming the cell it reaches, on an Erlang build as on any other.

Cells in this repository that prove it: none yet — `json` holds no code and no cell beside its decision cells until 144 B-27 and 151 s1 move std's `json.bp` here.

[draft/main.bp](draft/main.bp)
