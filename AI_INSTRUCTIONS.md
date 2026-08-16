# Development workflow

## Workflow
- Check `./.ai-instructions/docs/technology` for rules and conventions. You are required to follow them, and to learn them before starting work. If you find a rule that is seems wrong for the project, raise it with the user before starting work.
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


## IMPORTANT
- If you find that the main repository has code review subagents (in `.codex` or `.claude`) you are required to run them roughly every 800 changed lines and before risky refactors. After you make fixes, run the code review subagents again to ensure that your changes are acceptable.

## Engineering principles

- Every answer must be heavily supported by detailed investigation — don't rush to a conclusion.
- When an answer depends on, or would be meaningfully improved by, online information, search it out.
  Weigh only highly reputable sources the relevant specialist community accepts as trustworthy; disregard
  the rest.
- Prove requested functionality with tests. 100% code coverage isn't required; 100% requirement and result
  coverage is.
