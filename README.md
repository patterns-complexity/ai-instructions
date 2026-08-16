# Shared AI instructions

This repository contains shared instructions for AI coding tools. Add it to a project once, then link to it from that project instead of copying the same rules into every repository.

It supports Codex and Claude Code.

## Add these instructions to a project

### Add this repository as a Git submodule

1. From your project's root, add this repository as a Git submodule:

   ```sh
   git submodule add <shared-instructions-repository-url> .ai-instructions
   ```

2. In your project, confirm that only the submodule reference and `.gitmodules` file are staged:

   ```sh
   git status --short
   ```

   The output should show `.ai-instructions` and `.gitmodules` as added files.

3. In your project, commit the submodule reference and `.gitmodules` file:

   ```sh
   git commit -m "Add shared AI instructions"
   ```

4. From your project's root, initialize the submodule:

   ```sh
   git submodule update --init --recursive
   ```

### When cloning a project that includes this repository as a submodule

1. Clone your project:

   ```sh
   git clone <project-repo-url>
   ```

2. From your project's root, initialize the submodule after cloning or after pulling a commit that adds or updates the submodule:

   ```sh
   git submodule update --init --recursive
   ```

### Choose the section for the AI tool you use

#### Codex

1. Find `AGENTS.md` in your project's root. Create it if it does not exist.

2. Add the following text to `AGENTS.md`:

   ```markdown
   ## Shared instructions

   Also follow the shared engineering workflow and ruleset at `.ai-instructions/AI_INSTRUCTIONS.md` and `.ai-instructions/docs/technology/rules/README.md`.
   ```

3. If Cortex MCP is already configured in your project, replace the text from step 2 with this version:

   ```markdown
   ## Shared instructions

   Also follow the shared engineering workflow and ruleset at `.ai-instructions/AI_INSTRUCTIONS.md` and `.ai-instructions/docs/technology/rules/README.md`. Always use the Cortex MCP tools for code discovery, as described in `.ai-instructions/MCP_CORTEX_USAGE.md`.
   ```

#### Claude Code

1. Find `CLAUDE.md` in your project's root. Create it if it does not exist.

2. Add this line to `CLAUDE.md`:

   ```markdown
   @.ai-instructions/AI_INSTRUCTIONS.md
   ```

3. If Cortex MCP is already configured in your project, also add this line:

   ```markdown
   @.ai-instructions/MCP_CORTEX_USAGE.md
   ```

## If you use Explore or Plan in Claude Code

Claude Code’s built-in Explore and Plan agents do not load the instructions in your project’s `CLAUDE.md`.

1. In your project, check whether these files already exist:

   - `.claude/agents/project-explore.md`
   - `.claude/agents/project-plan.md`

2. From your project's root, run only the command for a file that is missing:

   > **Important:** If either file already exists in your project, do not run its symlink command. Compare it with the matching file in the shared repository at `.ai-instructions/.claude/agents/` and copy any wanted settings manually.

   ```sh
   # Safe to run even if the folder already exists.
   mkdir -p .claude/agents

   # Run only if .claude/agents/project-explore.md is missing.
   ln -s ../../.ai-instructions/.claude/agents/project-explore.md .claude/agents/project-explore.md

   # Run only if .claude/agents/project-plan.md is missing.
   ln -s ../../.ai-instructions/.claude/agents/project-plan.md .claude/agents/project-plan.md
   ```

3. Restart Claude Code after adding the agents to your project. Claude Code may delegate to them automatically. To invoke one explicitly, mention its name in your prompt or use `@agent-project-explore` or `@agent-project-plan`.

## [Recommended but optional] Code reviewer agents

### Codex

The shared repository includes these Codex files for a code reviewer:

- `.ai-instructions/.codex/config.toml`
- `.ai-instructions/.codex/agents/code-reviewer.toml`

To use them, Codex needs these files in your project:

- `.codex/config.toml`
- `.codex/agents/code-reviewer.toml`

1. In your project, check whether these files already exist:

   - `.codex/config.toml`
   - `.codex/agents/code-reviewer.toml`

2. From your project's root, run only the command for a file that is missing:

   > **Important:** If either file already exists in your project, do not run its symlink command. Compare it with the matching file in the shared repository at `.ai-instructions/.codex/` and copy any wanted settings manually.

   ```sh
   # Safe to run even if the folder already exists.
   mkdir -p .codex/agents

   # Run only if .codex/config.toml is missing.
   ln -s ../.ai-instructions/.codex/config.toml .codex/config.toml

   # Run only if .codex/agents/code-reviewer.toml is missing.
   ln -s ../../.ai-instructions/.codex/agents/code-reviewer.toml .codex/agents/code-reviewer.toml
   ```

3. In your project's `AGENTS.md`, add the following text:

   ```markdown
   ## Code reviewer workflow

   Also follow the code reviewer workflow at `.ai-instructions/CODE_REVIEWER_INSTRUCTIONS.md`.
   ```

### Claude Code

The shared repository includes these Claude Code files for a code reviewer:

- `.ai-instructions/.claude/agents/code-reviewer.md`
- `.ai-instructions/.claude/settings.local.json`

To use them, Claude Code needs these files in your project:

- `.claude/agents/code-reviewer.md`
- `.claude/settings.local.json`

1. In your project, check whether these files already exist:

   - `.claude/agents/code-reviewer.md`
   - `.claude/settings.local.json`

2. Keep your project's `.claude/settings.local.json` out of version control. In your project's `.gitignore`, add this line before creating the symlink. Create `.gitignore` if it does not exist:

   ```gitignore
   .claude/settings.local.json
   ```

3. From your project's root, run only the command for a file that is missing:

   > **Important:** If either file already exists in your project, do not run its symlink command. Compare it with the matching file in the shared repository at `.ai-instructions/.claude/` and copy any wanted settings manually.

   ```sh
   # Safe to run even if the folder already exists.
   mkdir -p .claude/agents

   # Run only if .claude/agents/code-reviewer.md is missing.
   ln -s ../../.ai-instructions/.claude/agents/code-reviewer.md .claude/agents/code-reviewer.md

   # Run only if .claude/settings.local.json is missing.
   ln -s ../.ai-instructions/.claude/settings.local.json .claude/settings.local.json
   ```

4. In your project's `CLAUDE.md`, add this line:

   ```markdown
   @.ai-instructions/CODE_REVIEWER_INSTRUCTIONS.md
   ```

## What is included

- [`AI_INSTRUCTIONS.md`](AI_INSTRUCTIONS.md)  
  The main workflow and engineering rules.

- [`MCP_CORTEX_USAGE.md`](MCP_CORTEX_USAGE.md)  
  Instructions for using Cortex MCP to find and inspect code. Use this only in projects that have Cortex MCP.

- [`CODE_REVIEWER_INSTRUCTIONS.md`](CODE_REVIEWER_INSTRUCTIONS.md)  
  Instructions for using the code reviewer agent. Use this only in projects that configure a code reviewer agent.

- [`docs/README.md`](docs/README.md)  
  Explains how the documentation is organised.

- [`docs/technology/README.md`](docs/technology/README.md)  
  An index of the technical rules.

- [`docs/technology/rules/README.md`](docs/technology/rules/README.md)  
  The detailed engineering rules, including architecture, code quality, performance, C++23, and Rust guidance.

- [`.claude/agents/code-reviewer.md`](.claude/agents/code-reviewer.md)  
  Review-agent settings for Claude Code.

- [`.claude/agents/project-explore.md`](.claude/agents/project-explore.md)  
  Project exploration agent settings for Claude Code.

- [`.claude/agents/project-plan.md`](.claude/agents/project-plan.md)  
  Project planning agent settings for Claude Code.

- [`.claude/settings.local.json`](.claude/settings.local.json)  
  Claude Code permissions for read-only Cortex MCP status tools.

- [`.codex/config.toml`](.codex/config.toml)  
  Main Codex settings, including its model, permissions, and network access.

- [`.codex/agents/code-reviewer.toml`](.codex/agents/code-reviewer.toml)  
  Review-agent settings for Codex.

The model names in the `.codex` files are working defaults, not examples. You can change them for a specific project if needed.
