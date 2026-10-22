---
name: google-rust-style-guide
description: Apply Google's Rust Style Guide when writing, reviewing, or refactoring Rust code, including API design, ownership, error handling, traits, documentation, and unsafe boundaries. Use for Google Rust style requests and Rust style reviews; distinguish library APIs from application code and preserve Chromium, Android, and Fuchsia scope restrictions.
license: CC-BY-3.0
metadata:
  author: StudentWeis
  version: "0.1.0"
  upstream-commit: 2ac1584cd3c9854760f02418ec24687ec1698fb8
---

# Google Rust Style Guide

Apply the [bundled Google Rust Style Guide](references/rustguide.md) to the code under discussion. This is an independent community skill, not an official Google product. The reference is a verbatim upstream snapshot; attribution and provenance are in [NOTICE.md](NOTICE.md).

## Establish scope

1. Read the target repository's instructions, formatter and lint configuration, toolchain/MSRV, and relevant surrounding code. Follow explicit user requirements and project policy; explain conflicts with this guide rather than silently replacing local conventions.
2. Identify whether the target is reusable library code or application code, and whether it actually belongs to Chromium, Android, or Fuchsia. Read **Apply API design rules in context** before changing an API. Within this guide, API rules are binding for libraries and strong recommendations for applications; application code should favor immediate needs and simplicity.
3. Read the applicable sections below, including their exceptions and rationale, before proposing a change. Treat headings as navigation, not complete rules. The bundled reference controls when this entrypoint's summary is incomplete.
4. Apply only rules relevant to the requested work. A style review does not authorize broad API migrations, new dependencies, or unrelated rewrites. Explain compatibility costs before proposing changes to public signatures or construction patterns.

## Find the relevant rules

Search the exact headings in `references/rustguide.md` and read through the next heading of equal or higher level. Paths are relative to this skill's directory, not the target repository. Load only the needed sections; for a comprehensive review, cover each relevant topic in turn.

| Task | Sections to read |
| --- | --- |
| Establish policy | Background; Follow public Rust style rules; Apply API design rules in context |
| Crates, modules, imports | Code organization |
| Formatting, rustfmt configuration | Code formatting and aesthetics |
| Borrowing, cloning, shared ownership | Ownership and borrowing |
| Parameters, iterators, errors | Function inputs and outputs |
| Newtypes and data representation | Types |
| Traits, derives, generics, dynamic dispatch | Traits |
| Mutexes, async, threads | Concurrency |
| Macros and code generation | Macros |
| Naming and constructors | Naming |
| Public docs, panic contracts, safety contracts | When and how to write documentation |
| Unsafe, unstable features, accessors, API evolution | Other Rust features |
| Matching, panics, inference, loops, assertions, strings | Implementation concerns |
| Test framework selection | Use the right per-codebase test framework |

For example, locate ownership rules with `rg -n '^## Ownership and borrowing|^## Function inputs and outputs' references/rustguide.md`, then read the intervening section with the available file reader. If `rg` is unavailable, use the file reader's search or another text search tool.

## Preserve conditions and exceptions

- **Ownership:** prefer unique ownership and borrowing. `Rc` and `Arc` remain appropriate when alternatives become unreasonably complex. Cloning a reference-counted pointer is not a deep copy; a deep clone can also be pragmatic when borrowing becomes excessively complex.
- **API flexibility:** library iterator and generic recommendations do not require application code to replace simple slices and vectors with generalized interfaces. Read the return-iterator exceptions and the code-size tradeoff for `impl Into<T>` and generics.
- **Booleans and traits:** use enum parameters when a boolean's purpose is unclear. Define traits for generic programming, dynamic dispatch, or justified extension methods, not merely to group methods.
- **Errors:** choose `Option`, `Result`, or panic according to the API contract. `expect` is for an unavoidable invariant panic, not a substitute for handling recoverable errors. Read the separate `catch_unwind` rule and its defense-in-depth exception before advising on panic recovery.
- **Public API evolution:** `#[non_exhaustive]` guidance concerns APIs used by other teams and includes exceptions for stable shapes, coordinated migrations, and struct update syntax. Do not add the attribute to every `pub` item mechanically; it can break downstream construction and matching.
- **Unsafe:** prefer safe implementations. When unsafe is necessary, require a technical justification, a safe abstraction where possible, and a `SAFETY:` explanation. Performance justifications need benchmarks. Style compliance alone does not establish soundness; inspect the actual safety contracts.
- **Platform rules:** Chromium's small crates, flat file layout, import mechanism, async prohibition, thread policy, and test framework are Chromium-specific. Fuchsia's mutex and test framework are Fuchsia-specific. Preserve ordinary Cargo layouts, async runtimes, and `#[test]` outside those codebases unless project policy says otherwise. Platform-specific exceptions can also appear inside otherwise general sections.
- **Toolchain:** do not switch to nightly or enable unstable formatter options or lints just to imitate the guide. Check availability on the project's toolchain. Upstream examples include illustrative fragments and may contain errors; validate code you generate instead of copying examples blindly.

## Implement or review

For implementation, make the smallest change that meets the task and applicable guidance. Preserve existing behavior unless a behavior change is requested. Explain material departures from the guide and why the project context warrants them.

For review, report actionable findings with the target file and line, the relevant guide section, its applicability, and a concrete correction. Separate correctness problems, applicable style rules, and optional recommendations. Check exceptions before reporting a violation; do not label a scoped preference a Rust language requirement. If no actionable issue remains, say so without inventing findings.

Use the repository's validation entrypoints. In a conventional Cargo project without custom wrappers, select appropriate checks from `cargo fmt --check`, `cargo clippy`, and `cargo test`, with the project's supported packages, targets, and features. Do not enable all features indiscriminately. Report what ran, what failed, and what could not be verified. Formatter and Clippy success do not establish full guide compliance.

## Sources and freshness

The bundled reference is pinned to Google styleguide commit `2ac1584cd3c9854760f02418ec24687ec1698fb8` (2026-10-21). Use it offline without claiming it is always the latest version. When asked for current guidance, consult the [live Google guide](https://google.github.io/styleguide/rustguide.html) and identify any differences from the snapshot. Do not silently edit the installed reference during an ordinary code task.

For matters the Google guide does not cover, consult the [Rust Style Guide](https://doc.rust-lang.org/style-guide/) and [Rust API Guidelines](https://rust-lang.github.io/api-guidelines/). Google-specific rules take precedence over these general guides only within the adopted Google style policy; explicit project requirements still control this skill's application.
