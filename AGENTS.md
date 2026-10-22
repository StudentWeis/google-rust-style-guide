# Maintenance

This repository packages one portable Agent Skill. Keep `SKILL.md` concise and use `references/rustguide.md` as the authoritative rule text. Avoid duplicating the full guide in summaries or adding requirements that the upstream guide does not impose.

## Updating the guide

1. Choose and inspect an explicit commit from `google/styleguide`. Retrieve `rustguide.md` at that commit and preserve its bytes in `references/rustguide.md`; do not apply local Markdown formatting to the vendored file.
2. Read the upstream diff, including exceptions, platform markers, and changed headings. Update the entrypoint's navigation and safeguards where needed. Preserve the distinction between library and application code.
3. Update the commit and date in `SKILL.md`, `README.md`, and `NOTICE.md`, and bump the skill version when its behavior or reference changes. Verify the upstream license still matches `LICENSE`.
4. Validate the package before committing. Do not describe a snapshot as the latest guide without checking upstream.

## Validation

- Check YAML frontmatter against the [Agent Skills specification](https://agentskills.io/specification): the name matches the directory, the description explains activation, and the entrypoint stays below the recommended 500 lines.
- Check Markdown structure and local links in authored documents. Exclude the unmodified upstream reference from local formatting rules; verify its bytes against the pinned source instead.
- Verify every navigation heading in `SKILL.md` exists in the reference and read the corresponding sections when modifying a summary.
- Use `npx skills add . --list` to check discovery without installing. Run `git diff --check` on authored changes. Upstream whitespace belongs to the preserved snapshot.
- When changing the workflow, exercise representative prompts with an available coding agent: an ordinary Cargo async application must not acquire Chromium restrictions; an application returning `Vec` must not be generalized without need; `Arc` cloning must not be mistaken for deep copying; public API evolution must retain the documented exceptions; unsafe performance claims must require justification and benchmarks. Distinguish actual agent trials from a manual review of these cases.

Keep the package usable without a network connection or executable helper scripts. Keep attribution and the license with any redistributed skill package. Upstream examples are source material, not a compilation test suite; validate newly generated Rust in the target project.
