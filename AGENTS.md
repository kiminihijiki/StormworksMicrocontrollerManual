# AI contributor guidance

This repository is the integration entry point for two Stormworks supplements. It is not a second source of truth for DSL, gate definitions, XML conversion, Lua runtime facts, or part data.

## Before generating code

- Read `docs/ai-workflow.md`.
- Use [stormworks-microcontroller-lua](https://github.com/kiminihijiki/stormworks-microcontroller-lua) for microcontroller Lua runtime and API guidance. Keep it separate from add-on Lua.
- Use [stormworks-partdata](https://github.com/kiminihijiki/stormworks-partdata) for part and sensor lookup. Use `--mcu-relevant` for MCU candidates and `--lua-relevant` for Lua I/O candidates.
- Use the external DSL/XML validation environment for `spec`, `check-dsl`, and `typecheck-dsl`.
- Write the external I/O contract before writing Lua. Part node order, Composite channel numbers, and MCU interface channel numbers are different.
- Do not invent Composite meanings, units, ranges, or unconfirmed game behavior.

## Repository boundaries

- Do not copy external DSL, gate, or XML definitions into this repository.
- Do not copy the part catalog or Lua runtime documents here; update the specialized repositories instead.
- Keep `data/sources.json` synchronized when the integration guide adopts a new revision.
- Preserve `docs/archive/` as historical material and do not treat it as the current specification.
