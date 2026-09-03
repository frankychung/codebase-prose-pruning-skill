# Language traps

Consult only the languages present in the target.

## Rust

- `//!` and `///` can contain doctests and shape generated API documentation.
- `//` and `/* */` may be data inside normal, byte, raw, or raw-byte strings.
- Removing a comment can make `rustfmt` reflow adjacent code; distinguish formatting from token changes.
- `SAFETY` comments may be the only local proof supporting an `unsafe` block.

## JavaScript and TypeScript

- Comment markers may occur inside strings, template literals, regular expressions, embedded source, and test fixtures.
- JSDoc may drive TypeScript checking, editors, documentation, or closure-style compilation.
- Preserve directives such as `@ts-check`, source-map links, coverage controls, bundler hints, and lint controls unless their effect is intentionally removed.
- A concise comment is justified when browser event ordering or silent morph behavior cannot be inferred locally.

## ReScript

- `/** ... */` documents the following declaration; `/*** ... */` is standalone documentation. Inspect its API role before pruning, especially in `.resi` files.
- Comment markers inside strings, multiline or tagged templates, and `%raw` or `%%raw` JavaScript are runtime data or executable source.
- `@...` and `@@...` attributes and `%...` and `%%...` extension points are compiler-significant code, not comments.
- `.resi` files define public module signatures and may be the API's documentation surface.
- Compiled JavaScript and genType `*.gen.tsx` files are generated output. Confirm provenance and configured suffixes, then edit the ReScript source or configuration.

Sources: [overview](https://rescript-lang.org/docs/manual/overview/), [attributes](https://rescript-lang.org/docs/manual/attribute/), [raw JavaScript](https://rescript-lang.org/docs/manual/embed-raw-javascript/), [modules and signatures](https://rescript-lang.org/docs/manual/module/), and [TypeScript integration](https://rescript-lang.org/docs/manual/typescript-integration/).

## CSS

- Keep comments explaining compatibility hacks whose declarations otherwise look removable.
- Preserve required license banners and build-tool directives.
- Section comments should describe genuine regions, not repeat the next selector.

## HTML, XML, and SVG

- Comments may carry attribution or generated-file provenance.
- XML forbids `--` inside comments.
- Edit a generator rather than its output when the output is generated.

## Python

- Docstrings are runtime objects, not comments. Their removal can affect introspection, documentation, tests, and tooling.
- Preserve shebangs, encoding declarations, type-checking directives, and lint/coverage controls.
- `#` inside strings and fixtures is data.

## Shell

- Preserve shebangs and shellcheck directives.
- Here-documents may contain apparent comments belonging to another language or to runtime data.

## Go

- Preserve build constraints and generation directives such as `//go:build` and `//go:generate`.
- Exported declarations may require comments under repository lint policy.

## C, C++, and unsafe systems code

- Preserve proofs about ownership, aliasing, lifetime, synchronization, ABI, and undefined behavior.
- Preprocessor-controlled comments and tool directives may affect generated documentation or static analysis.

## Tests and fixtures

- A test comment survives only when it explains a non-obvious fixture, timing bound, platform skip, assertion that appears redundant, or regression condition not captured by the test name.
- Comments embedded in fixture strings are fixture data even when they look like source comments.
