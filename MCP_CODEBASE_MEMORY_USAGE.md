# Code discovery: Codebase Memory MCP is mandatory

Every project's codebase is indexed via codebase-memory-mcp. Use `search_graph`, `trace_path`, `get_code_snippet`,
`query_graph`, `get_architecture` FIRST — every session, before grep/glob/file-search. Skip only when
literally impossible: MCP unreachable, target can't be indexed, or out of scope (see fallback list below).
"Habit" or "grep is faster" are never valid reasons to skip it.

- Priority: `search_graph` → `trace_path` → `get_code_snippet` → `query_graph` → `get_architecture`.
- Fall back to grep/glob only for: string literals/error messages/config values; non-code files (Dockerfiles,
  shell scripts, configs); or when the graph genuinely returns insufficient results after being tried.
- Every one of these calls takes a **required** `project` argument — the index name auto-derived from the
  repo path. Run `list_projects` if you don't know it.
- Examples: find a handler `search_graph(project="<name>", name_pattern=".*OrderHandler.*")`; find its
  callers `trace_path(project="<name>", function_name="OrderHandler", direction="inbound")`; read source
  `get_code_snippet(project="<name>", qualified_name="<name>.src.orders.OrderHandler")`.
- Qualified names are dot-separated and project-prefixed (e.g. `myproj.src.engine.src.main.main`), not
  path-style. Always take the exact string from `search_graph` output instead of constructing it by hand.
- If a project isn't indexed yet, run `index_repository` first. Never pass a custom `name` — let it
  auto-derive from the repo path, or you'll create a duplicate index. Check `list_projects` if unsure
  whether it's already indexed.
- Graph coverage is best-effort, never proof of completeness. Use `check_index_coverage` for every cited
  path and before any negative or exhaustive claim ("X has no callers", "nothing else uses Y"); `index_status`
  reports files that were skipped or only partially parsed. Grep inside those ranges rather than trusting
  a negative graph result.
- For git submodules or vendored dependencies that warrant their own index, index them as a separate
  project and query by name instead of grepping/reading their files directly; they may not surface in
  `list_projects` but still resolve when passed explicitly as `project=<name>`. Use a `.cbmignore` to
  exclude vendored third-party code that shouldn't be indexed at all.
- Even for repos outside the current one, check whether the graph has them indexed before falling back to grep.
