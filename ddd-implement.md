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
   - `specs/system.yaml` — project identity, tech stack, environments (if exists)
   - `specs/architecture.yaml` — conventions, infrastructure, API design (if exists)
   - `specs/config.yaml` — environment variable schema (if exists)
   - `specs/shared/errors.yaml` — error codes with HTTP status mappings (if exists)
   - `specs/schemas/*.yaml` — data model definitions referenced by data_store nodes in the flow (if exist)
   - `specs/domains/{domain}/domain.yaml` — domain context, events, relationships
   - `specs/domains/{domain}/flows/{flow}.yaml` — the flow specification

4. **Understand the flow spec**: Each flow YAML contains:
   - `flow:` — metadata (id, name, type, domain)
   - `trigger:` — what starts the flow (event, HTTP, scheduled, manual)
   - `nodes:` — ordered list of processing steps with types:
     - `input` — user/external input with validation rules
     - `process` — business logic step
     - `decision` — branching point (connections have labels like "Yes"/"No")
     - `terminal` — end state (with optional `status` and `body` for HTTP responses)
     - `data_store` — database operation (CRUD, with optional `pagination`/`sort` for reads)
     - `service_call` — external API call (with optional `error_mapping` for status→error code)
     - `event` — publish/subscribe event
     - `loop` — iteration over a collection
     - `parallel` — concurrent processing
     - `sub_flow` — reference to another flow
     - `llm_call` — single LLM invocation
     - `agent_loop` — LLM agent with tools in a loop
     - `guardrail` — input/output validation for agent flows
     - `human_gate` — async human approval step for agent flows
     - `orchestrator` — multi-agent supervisor/coordinator
     - `smart_router` — rule-based or LLM-based routing to agents
     - `handoff` — transfer/consult/collaborate between agents
     - `agent_group` — group of agents working together
   - Each node has `connections:` listing target nodes with `sourceHandle` for branching nodes
   - Each node has `spec:` with type-specific configuration fields
   - Each node may have `observability:` (logging, metrics, tracing) and `security:` (auth, rate limiting, encryption, audit) configs

5. **Check existing implementation**: Read `.ddd/mapping.yaml` to see if this flow was previously implemented.
   - If yes and spec hasn't changed → skip (tell user it's up to date)
   - If yes and spec changed → update mode (modify existing files, don't recreate)
   - If no → new implementation

6. **Implement**:

   **Entry point — determine from trigger convention**:
   - `HTTP {METHOD} {path}` → route handler (e.g., Express route, FastAPI endpoint)
   - `cron {expression}` → scheduled job (e.g., node-cron, BullMQ repeatable)
   - `event:{EventName}` → event listener/consumer (e.g., message queue subscriber)
   - `webhook {path}` → webhook handler route
   - `manual` → CLI command or admin endpoint

   **Follow the node graph** from trigger through all paths to terminal nodes. Each node becomes real code:
   - `process` → service function call
   - `decision` → if/else or switch using the `condition` field
   - `data_store` → database query (ORM call matching `operation`: create/read/update/delete on `model`)
   - `service_call` → HTTP client call (method, url, headers, body, timeout, retry)
   - `event` → event emission (emit) or subscription handler (consume)
   - `loop` → for/forEach over `collection` with `iterator` variable, optional `break_condition`
   - `parallel` → Promise.all / concurrent execution of branches
   - `sub_flow` → call to the referenced flow's entry function
   - `llm_call` → LLM API call with model, prompt, temperature, structured output
   - `agent_loop` → agent loop with tool dispatch, memory management, stop conditions
   - `guardrail` → validation middleware (inline, sequential — input guard before agent, output guard after)
   - `human_gate` → async approval workflow (pause, notify, wait for human decision)
   - `orchestrator` → multi-agent coordination per `strategy` (supervisor, round_robin, broadcast, consensus)
   - `smart_router` → routing logic from `rules` and/or `llm_routing`
   - `handoff` → agent transfer with context passing per `mode` (transfer/consult/collaborate)
   - `agent_group` → agent team coordination with shared memory

   **Wire connections using `sourceHandle`** — nodes with multiple output paths use `sourceHandle` values:
   - `input` → `"valid"` path (continue) / `"invalid"` path (validation error terminal)
   - `decision` → `"true"` path / `"false"` path
   - `data_store` → `"success"` path (continue) / `"error"` path (DB error terminal)
   - `service_call` → `"success"` path (continue) / `"error"` path (use `error_mapping` to map HTTP status codes to error codes)
   - `loop` → `"body"` path (loop body) / `"done"` path (after loop completes)
   - `parallel` → `"branch-0"`, `"branch-1"`, etc. (parallel branches) / `"done"` path (join point)
   - `smart_router` → dynamic route names as handle IDs

   **Terminal nodes → HTTP responses**: Use `status` and `body` fields from terminal spec:
   - `status` → HTTP status code (e.g., 201, 400, 409)
   - `body` → response body shape (values starting with `$.` are variable references)
   - Map `body.error` values to error codes defined in `specs/shared/errors.yaml` for consistent error responses

   **Data store pagination/sort**: When `data_store` has `operation: read` with `pagination` and/or `sort` fields:
   - Implement cursor-based or offset pagination per `pagination.style`
   - Apply sort ordering per `sort.default` and `sort.allowed`
   - Accept pagination/sort query parameters in the route handler

   **Cross-cutting concerns**: If a node has `observability` or `security` config:
   - `observability.logging` → add structured logging at the specified level, include/exclude input/output
   - `observability.metrics` → instrument with counters/histograms for the custom counters listed
   - `observability.tracing` → add tracing spans with the specified span name
   - `security.authentication` → add auth middleware (methods, required roles)
   - `security.rate_limiting` → add rate limiting middleware (requests per minute)
   - `security.encryption` → encrypt PII fields at rest, ensure TLS in transit
   - `security.audit` → add audit logging for the operation

   **Follow architecture conventions**: Use `specs/architecture.yaml` to shape generated code:
   - `project_structure` → place files in the correct directories
   - `naming_conventions` → use the right casing for files, classes, functions, variables, tables, endpoints
   - `dependencies` → use the specified libraries and versions
   - `api_design` → follow versioning, pagination format, filtering style, error format
   - `testing` → use the specified framework, runner, and patterns

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
