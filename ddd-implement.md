# DDD Implement

Implement DDD-designed flows from the specs directory. Supports implementing the entire project, a specific domain, or a specific flow.

## Scope Resolution

Parse the argument to determine scope:

| Argument | Scope | Example |
|----------|-------|---------|
| `--all` | Whole project — all domains, all flows | `/ddd-implement --all` |
| `domain-name` | All flows in a domain | `/ddd-implement users` |
| `domain-name/flow-name` | Single flow | `/ddd-implement users/user-registration` |
| *(empty)* | Interactive — list available flows and ask | `/ddd-implement` |

## Instructions

1. **Find the DDD project**: Look for `ddd-project.json` in the current directory or parent directories. This file lists all domains and project configuration (tech stack, etc.).

2. **Resolve the scope from the argument**:

   **If no argument**: List all domains and their flows with implementation status (check `.ddd/mapping.yaml`). Show which are implemented (with date), which have drift, and which are new. Ask the user what to implement.

   **If `--all`**: Collect all flows across all domains. Implement them in dependency order (flows that publish events before flows that consume them).

   **If `domain-name`**: Read `specs/domains/{domain-name}/domain.yaml` to get the flow list. Implement all flows in that domain.

   **If `domain-name/flow-name`**: Read `specs/domains/{domain-name}/flows/{flow-name}.yaml`. Implement just that flow.

3. **Read the specs for each flow**:
   - `ddd-project.json` — project config, tech stack
   - `specs/domains/{domain}/domain.yaml` — domain context, events, relationships
   - `specs/domains/{domain}/flows/{flow}.yaml` — the flow specification

4. **Understand the flow spec**: Each flow YAML contains:
   - `flow:` — metadata (id, name, type, domain)
   - `trigger:` — what starts the flow (event, HTTP, scheduled, manual)
   - `nodes:` — ordered list of processing steps with types:
     - `input` — user/external input with validation rules
     - `process` — business logic step
     - `decision` — branching point (connections have labels like "Yes"/"No")
     - `terminal` — end state
     - `data_store` — database operation (CRUD)
     - `service_call` — external API call
     - `event` — publish/subscribe event
     - `loop` — iteration over a collection
     - `parallel` — concurrent processing
     - `sub_flow` — reference to another flow
     - `agent_loop` — LLM agent with tools
     - `guardrail` — input/output validation
     - `human_gate` — human approval step
   - Each node has `connections:` listing target nodes (with optional labels for decision branches)
   - Each node has `spec:` with type-specific configuration fields

5. **Check existing implementation**: Read `.ddd/mapping.yaml` to see if this flow was previously implemented.
   - If yes and spec hasn't changed → skip (tell user it's up to date)
   - If yes and spec changed → update mode (modify existing files, don't recreate)
   - If no → new implementation

6. **Implement**:
   - Follow the node graph from trigger through all paths to terminal nodes
   - Each node becomes real code (route handler, service function, DB query, etc.)
   - Wire connections as function calls, conditionals, or event emissions
   - Decision nodes become if/else or switch statements with the connection labels as conditions
   - Match the project's existing code style and conventions
   - For multi-flow implementations, share common infrastructure (DB, config, middleware)

7. **Write tests**: Create tests covering:
   - Happy path through the flow
   - Each decision branch
   - Error/terminal states
   - Input validation rules from input node specs

8. **Run tests and fix**: Run the test suite. If tests fail, fix the implementation. Keep iterating until all tests pass.

9. **Update mapping**: After each flow is successfully implemented, update `.ddd/mapping.yaml`:
   ```yaml
   flows:
     domain-id/flow-id:
       specHash: (sha256 of the flow YAML content)
       implementedAt: (current ISO timestamp)
       files:
         - src/path/to/file1.ts
         - src/path/to/file2.ts
   ```

10. **Summary**: After all flows are done, show a summary table:
    ```
    Domain/Flow                  Status    Files  Tests
    users/user-registration      ✓ done    5      12/12
    users/user-login             ✓ done    3      8/8
    billing/create-subscription  ✓ done    4      6/6
    ```

$ARGUMENTS
