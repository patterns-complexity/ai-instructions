# Code discovery: Cortex MCP is mandatory

Every project's codebase is indexed via code-cortex-mcp. Use `search_graph`, `trace_path`, `get_code_snippet`,
`query_graph`, `get_architecture` FIRST — every session, before grep/glob/file-search. Skip only when
literally impossible: MCP unreachable, target can't be indexed, or out of scope (see fallback list below).
"Habit" or "grep is faster" are never valid reasons to skip it.

- Priority: `search_graph` → `trace_path` → `get_code_snippet` → `query_graph` → `get_architecture`.
- Fall back to grep/glob only for: string literals/error messages/config values; non-code files (Dockerfiles,
  shell scripts, configs); or when Cortex genuinely returns insufficient results after being tried.
- Examples: find a handler `search_graph(name_pattern=".*OrderHandler.*")`; find its callers
  `trace_path(function_name="OrderHandler", direction="inbound")`; read source
  `get_code_snippet(qualified_name="pkg/orders.OrderHandler")`.
- If a project isn't indexed yet, run `index_repository` first. Never pass a custom `name` — let it
  auto-derive from the repo path, or you'll create a duplicate index. Check `list_projects` if unsure
  whether it's already indexed.
- For git submodules or vendored dependencies that warrant their own index, index them as a separate
  project and query by name instead of grepping/reading their files directly; they may not surface in
  `list_projects` but still resolve when passed explicitly as `project=<name>`. Use a `.cbmignore` to
  exclude vendored third-party code that shouldn't be indexed at all.
- Even for repos outside the current one, check whether Cortex has them indexed before falling back to grep.
