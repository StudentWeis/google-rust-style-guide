# Google Rust Style Guide skill

An Agent Skill for writing and reviewing Rust with [Google's Rust Style Guide](https://google.github.io/styleguide/rustguide.html). It includes a compact task-oriented entrypoint and a complete, pinned copy of the upstream guide for offline use.

**Community-maintained; not affiliated with or endorsed by Google.**

## Install

With Node.js and the [Skills CLI](https://github.com/vercel-labs/skills):

```sh
npx skills add StudentWeis/google-rust-style-guide --skill google-rust-style-guide
```

Select your agent and installation scope when prompted. To inspect available skills without installing:

```sh
npx skills add StudentWeis/google-rust-style-guide --list
```

For manual installation, copy this repository into a skill directory supported by your agent. Keep `SKILL.md`, `references/`, `NOTICE.md`, and `LICENSE` together; copying only `SKILL.md` loses the guide and attribution.

## Use

Ask your agent, for example:

- “Use google-rust-style-guide to review this Rust diff. Explain which rules apply and include their exceptions.”
- “Design this library API using Google's Rust style guidance without breaking existing callers.”
- “Check this Cargo application against Google's Rust guide, keeping its Tokio runtime and project conventions.”

The skill identifies library versus application code, reads only the relevant guide sections, and preserves platform-specific scope. It covers API design, ownership, imports, traits, error handling, documentation, unsafe code, and implementation style. It does not treat Chromium's async prohibition or flat file layout as universal Rust rules.

Project requirements take precedence. This skill supplies guidance; it is not a linter, a Rust compiler, or a proof of unsafe-code soundness.

## Contents

| File | Purpose |
| --- | --- |
| [SKILL.md](SKILL.md) | Skill metadata, navigation, scope rules, and workflow |
| [references/rustguide.md](references/rustguide.md) | Unmodified Google guide, including rationale and exceptions |
| [NOTICE.md](NOTICE.md) | Attribution and exact upstream provenance |
| [AGENTS.md](AGENTS.md) | Maintenance and validation instructions |

The reference is pinned to upstream commit [`2ac1584`](https://github.com/google/styleguide/commit/2ac1584cd3c9854760f02418ec24687ec1698fb8), dated 2026-10-21. It is not automatically synchronized. See the [live guide](https://google.github.io/styleguide/rustguide.html) for subsequent changes.

## License

The Google guide and this repository's original skill material are available under [Creative Commons Attribution 3.0 Unported](LICENSE). See [NOTICE.md](NOTICE.md) for attribution. Google retains attribution for the original guide; the skill's workflow and packaging are by StudentWeis.
