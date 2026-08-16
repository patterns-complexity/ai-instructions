# Development workflow

## Workflow

- The top-level agent implements every feature.
- Before any change, review `./docs/user` (if present) for the application's full scope and future features.
- Derive quality gates from version-controlled manifests, lockfiles, tool config, task runners, and CI — use
  their pinned commands/versions; never assume a language, build system, package manager, or analysis tool.
- During implementation, run applicable fast checks (formatting, parsing, linting, type checking, other
  static analysis, compilation, generated-code consistency) roughly every 800 changed lines and before risky
  refactors, across every affected language, production code, tests, scripts, migrations, build logic, and
  configuration.
- Before handoff, run the full configured suite for the affected scope, then repo-wide when practical: tests
  plus every formatter, linter, static analyzer, compiler/build check, doc/link checker, config/schema
  validator, architecture rule, dependency audit, security scanner, secret scanner, and license/provenance
  check. Tests complement these; they don't replace them.
- Treat diagnostics/warnings as failures unless the repo records an accepted baseline. Fix root causes, not
  suppressions; keep any unavoidable suppression narrow and explain its safety. Don't swap quality tools
  just to satisfy this workflow. If a check can't run or has a pre-existing failure, report its exact
  command, affected scope, and failure evidence.
- Don't write technology documentation before implementation.

## Engineering principles

- Every answer must be heavily supported by detailed investigation — don't rush to a conclusion.
- When an answer depends on, or would be meaningfully improved by, online information, search it out.
  Weigh only highly reputable sources the relevant specialist community accepts as trustworthy; disregard
  the rest.
- Put configurable parameters in an `.env` file. Don't add a variable that's inferable from a simpler one;
  abstract a variable out only when doing so still leaves the user with full control over the result.
- Prove requested functionality with tests. 100% code coverage isn't required; 100% requirement and result
  coverage is.
