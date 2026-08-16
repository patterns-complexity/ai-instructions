# Code reviewer workflow

Use this file only in projects that configure a `code_reviewer` agent.

- The top-level agent invokes the `code_reviewer` sub-agent for a final review roughly every 400 changed lines, only after finishing a self-contained part. Intervals may run longer. Only request the final review once the whole feature is implemented.
- The `code_reviewer` checks strictly against all rules in `./docs/technology`. Fix every mismatch before re-requesting review. This is the workflow's most important gate; never hand off before it passes.
- Follow the technology documentation regardless of review outcome. Learn it before starting, since every review costs tokens and money.
- The `code_reviewer` must also incrementally judge whether new features require reorganizing old code, including moving related old and new objects into a better directory together.
- The `code_reviewer` only reviews code. It must never run builds.
