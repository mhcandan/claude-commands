# DDD Reverse

Reverse-engineer an existing codebase into a complete DDD (Design Driven Development) project. Scans source code and generates all YAML spec files that the DDD Tool can visualize and `/ddd-implement` can verify via round-trip.

## Input

Parse `$ARGUMENTS` for:
- **Project path** (required) — path to the source code to reverse-engineer
- `--output <path>` — where to write specs (default: same project directory)
- `--domains <d1,d2>` — only reverse-engineer specific domains (partial mode)
- `--merge` — merge with existing specs instead of overwriting

If no project path is provided, ask the user for it.

## Instructions

### Phase 1: Fetch spec reference + detect tech stack

1. **Fetch the DDD Usage Guide**: Run `gh api repos/mhcandan/DDD/contents/DDD-USAGE-GUIDE.md --jq '.content' | base64 -d` to get the latest version. This guide defines all YAML formats, node types, spec fields, connection patterns, and conventions. It is your primary reference for creating correct specs.

2. **Detect tech stack**: Read project configuration files to identify the stack:
   - `package.json` / `tsconfig.json` — Node.js/TypeScript, framework (Express, Fastify, NestJS, Next.js, Hono, etc.), dependencies
   - `Cargo.toml` — Rust, framework (Actix, Axum, Rocket, etc.)
   - `go.mod` — Go, framework (Gin, Echo, Fiber, Chi, etc.)
   - `requirements.txt` / `pyproject.toml` / `Pipfile` — Python, framework (FastAPI, Django, Flask, etc.)
   - `Gemfile` — Ruby, framework (Rails, Sinatra, etc.)
   - `pom.xml` / `build.gradle` — Java/Kotlin, framework (Spring Boot, etc.)
   - Also detect: database (Postgres, MySQL, MongoDB, Redis, etc.), ORM (Prisma, TypeORM, Drizzle, SQLAlchemy, Django ORM, GORM, etc.), cache, queue (Bull, RabbitMQ, Kafka, SQS, etc.), auth method

3. **Read environment and infrastructure**:
   - `.env` / `.env.example` / `.env.sample` — environment variables
   - `Dockerfile` / `docker-compose.yml` / `docker-compose.yaml` — infrastructure, services
   - `Procfile` / `fly.toml` / `vercel.json` / `netlify.toml` — deployment config

4. **Handle monorepos**: If the project root contains `packages/`, `apps/`, or a `workspaces` field in package.json, ask the user which package/app to reverse-engineer. If a `--domains` flag targets specific packages, proceed with those.

### Phase 2: Discover project structure + infer domains

5. **Scan source directory structure**: Explore the main source directories (`src/`, `app/`, `lib/`, `server/`, `api/`, `internal/`, `pkg/`, etc.) to understand the project layout.

6. **Identify domain boundaries**: Look for groupings that suggest bounded contexts:
   - **Feature folders**: `src/users/`, `src/orders/`, `src/products/`
   - **Module folders**: `modules/auth/`, `modules/billing/`
   - **Route groups**: `routes/users.ts`, `routes/orders.ts`
   - **Service classes**: `services/UserService`, `services/OrderService`
   - **Django apps**: each app directory
   - **NestJS modules**: each module directory
   - **Go packages**: each package under `internal/` or `pkg/`
   - **Microservices**: each service directory becomes its own domain

7. **Confirm domains with user**: Present the inferred domain groupings and ask the user to confirm or adjust:
   ```
   Inferred domains:
     1. users — src/users/, src/services/UserService, routes/users.ts
     2. orders — src/orders/, src/services/OrderService, routes/orders.ts
     3. notifications — src/notifications/, src/services/NotificationService

   Does this look right? Should I split, merge, or rename any domains?
   ```
   If the `--domains` flag was provided, only process those domains.

8. **Map domain ownership**: For each domain, record which source folders, files, and resources belong to it.

### Phase 3: Extract data models as schemas

9. **Find data model definitions**: Search for ORM/schema files:
   - Prisma: `schema.prisma` (parse `model` blocks)
   - TypeORM: files with `@Entity()` decorator
   - Drizzle: files using `pgTable()`, `mysqlTable()`, `sqliteTable()`
   - Sequelize: files using `sequelize.define()` or `Model.init()`
   - Mongoose: files using `new Schema()` or `mongoose.model()`
   - SQLAlchemy: classes inheriting `Base` or `db.Model`
   - Django: classes inheriting `models.Model`
   - GORM: structs with `gorm` tags
   - ActiveRecord: classes inheriting `ApplicationRecord`
   - Raw SQL: `migrations/` folder for schema definitions
   - If no ORM, look for TypeScript interfaces/types or JSON schemas that represent data models

10. **For each model, extract**:
    - Fields: name, type (map to generic types: string, integer, float, boolean, datetime, json, enum, relation), constraints (required, unique, default)
    - Relationships: belongs_to, has_many, has_one, many_to_many (with foreign key and related model)
    - Indexes: fields, unique flag
    - Lifecycle/status fields: if a field has a finite set of values (enum or string with known values), detect state transitions from code that updates this field
    - Timestamps: created_at, updated_at, deleted_at (soft delete)

11. **Generate schema specs**:
    - Create `specs/schemas/_base.yaml` with common fields (id, created_at, updated_at, deleted_at if soft deletes detected)
    - Create `specs/schemas/{model}.yaml` for each model
    - Map which domain owns which schemas (based on where the model is imported/used most)

### Phase 4: Extract flows from code

12. **Scan for entry points in each domain**:

    **HTTP routes/handlers**:
    - Express/Fastify/Hono: `router.get()`, `app.post()`, etc.
    - NestJS: `@Get()`, `@Post()`, etc. decorators on controller methods
    - Django: `urlpatterns`, `@api_view`, ViewSet methods
    - FastAPI: `@app.get()`, `@router.post()`, etc.
    - Rails: `routes.rb` + controller actions
    - Spring: `@GetMapping`, `@PostMapping`, etc.
    - Go: `r.HandleFunc()`, `e.GET()`, handler functions
    - Next.js: `app/api/*/route.ts` or `pages/api/*.ts`

    For each route: create a flow with trigger `HTTP {METHOD} {path}`.

    **Scheduled jobs/cron**:
    - Bull/BullMQ: `queue.process()`, `@Processor()`
    - node-cron/cron: `cron.schedule()`, `new CronJob()`
    - Celery: `@celery.task`, `@periodic_task`
    - Django: management commands, django-celery-beat
    - Spring: `@Scheduled`
    - Go: `cron.AddFunc()`

    For each job: create a flow with trigger `cron {expression}` and add `job_config` to trigger spec.

    **Event listeners/consumers**:
    - EventEmitter: `.on('eventName')`, `.addEventListener()`
    - Kafka/RabbitMQ consumers: `consumer.subscribe()`, `@Subscribe()`
    - Redis Pub/Sub: `subscriber.subscribe()`
    - AWS SQS/SNS: handler functions
    - Domain events: custom event bus patterns

    For each listener: create a flow with trigger `event:{EventName}`.

    **WebSocket/SSE handlers**: Create flows with trigger `ws {path}` or `sse {path}`.

13. **Trace execution paths**: For each entry point, read the handler function and trace through called functions/methods to build the node graph:

    - **Validation logic** (Joi, Zod, class-validator, Pydantic, manual checks) → `input` node with fields and validation rules
    - **Authorization checks** (middleware, decorators, guards) → `decision` node or security annotation
    - **Database reads/writes** (ORM calls, raw queries) → `data_store` node with `operation` (create/read/update/delete/upsert), `model`, and `query`/`data`
    - **External API calls** (fetch, axios, HttpService, requests) → `service_call` node with `method`, `url`, `headers`, `error_mapping`
    - **Conditional branches** (if/else, switch/case, ternary) → `decision` node with `condition`, wire both `true` and `false`
    - **Loops/iteration** (for, forEach, map over collections) → `loop` node with `collection` and `iterator`
    - **Parallel operations** (Promise.all, asyncio.gather, goroutines) → `parallel` node
    - **Event publishing** (emit, publish, dispatch) → `event` node with `direction: emit`
    - **LLM/AI calls** (OpenAI, Anthropic, LangChain, etc.) → `llm_call` node with `model` and `prompt_template`
    - **Sub-routine calls** (calling another flow's handler) → `sub_flow` node with `flow_ref`
    - **Response/return** (res.json, return Response, ctx.JSON) → `terminal` node with `outcome`, `status`, `body`
    - **Error handling** (try/catch, error middleware, rescue) → `terminal` node on error paths with appropriate error code

14. **Wire connections**: Connect nodes with proper `sourceHandle` values:
    - `input` → `"valid"` / `"invalid"`
    - `decision` → `"true"` / `"false"`
    - `data_store` → `"success"` / `"error"`
    - `service_call` → `"success"` / `"error"`
    - `loop` → `"body"` / `"done"`
    - `parallel` → `"branch-0"`, `"branch-1"`, ... / `"done"`
    - All other nodes → single output connection

15. **Position nodes**: Place nodes vertically with ~130px spacing. Branch error/invalid terminals to the right (x + 250). Start trigger at y=0.

### Phase 5: Extract cross-cutting concerns

16. **Error codes and constants**:
    - Find error code definitions, HTTP status mappings, error message constants
    - Generate `specs/shared/errors.yaml` with at minimum: VALIDATION_ERROR, UNAUTHORIZED, FORBIDDEN, NOT_FOUND, DUPLICATE_ENTRY, RATE_LIMITED, INTERNAL_ERROR
    - Add any project-specific error codes found in the source

17. **Shared types and enums**:
    - Find enums, constants, and value objects reused across 2+ domains
    - Generate `specs/shared/types.yaml`

18. **Architecture conventions**:
    - Infer project structure patterns, naming conventions (file naming, function naming), layer architecture (controller/service/repository)
    - Detect testing framework and patterns
    - Generate `specs/architecture.yaml`

19. **Configuration**:
    - Collect all environment variables from `.env.example`, `process.env` references, `os.environ`, config files
    - Categorize as required vs optional, group by concern (database, auth, external services, etc.)
    - Generate `specs/config.yaml`

20. **System-level spec**:
    - Generate `specs/system.yaml` with project identity, tech stack, environments
    - If external integrations are detected (third-party APIs, payment providers, email services, etc.), add an `integrations` section with base_url, auth, rate_limits, retry, timeout_ms per integration

### Phase 6: Wire events across domains

21. **Map event publishing**: For each `event` node with `direction: emit`, add an entry to the owning domain's `publishes_events` in `domain.yaml`:
    - `name`: the event name
    - `from_flow`: the flow that publishes it
    - `payload`: infer the event data shape from what's passed to the emit/publish call

22. **Map event consumption**: For each flow triggered by `event:{EventName}`, add to the consuming domain's `consumes_events`:
    - `name`: the event name
    - `handled_by_flow`: the flow that processes it

23. **Cross-reference**: Match publishers to consumers across domains. Flag any unmatched events:
    - Events published but never consumed → warning
    - Events consumed but never published → warning (may come from external systems)

### Phase 7: Quality checks + output

24. **Handle existing specs** (if output directory already has DDD files):
    - Without `--merge`: warn the user that specs will be overwritten, ask for confirmation
    - With `--merge`: read existing specs, preserve them, only add new domains/flows/schemas that don't already exist. If a flow already exists in specs, skip it (don't overwrite)

25. **Quality checks**: Before writing files, verify:
    - Every flow has exactly one trigger
    - All paths from trigger reach a terminal node (no dead ends)
    - No orphaned nodes (all reachable from trigger)
    - Decision nodes have both true and false branches wired
    - Input nodes have valid/invalid paths wired
    - Data store nodes have success/error paths wired
    - Service call nodes have success/error paths wired
    - Terminal nodes have `status` and `body` for HTTP-triggered flows
    - Error terminals reference error codes from `specs/shared/errors.yaml`
    - Published events have matching consumers across domains (or note warnings)
    - Schema models referenced by `data_store` nodes exist in `specs/schemas/`
    - Shared enums referenced by schemas exist in `specs/shared/types.yaml`

26. **Generate `ddd-project.json`**: List all domains with name and description.

27. **Write all spec files** to the output directory using the standard structure:
    ```
    {output}/
      ddd-project.json
      specs/
        system.yaml
        architecture.yaml
        config.yaml
        shared/
          errors.yaml
          types.yaml (if shared enums exist)
        schemas/
          _base.yaml
          {model}.yaml
        domains/
          {domain-id}/
            domain.yaml
            flows/
              {flow-id}.yaml
    ```

28. **Node ID convention**: Use `{type}-{8-char-random}` format (e.g., `input-xK9mR2vL`, `process-aPq3nW8j`).

29. **Summary**: After creating all files, show:
    ```
    Reverse-engineered DDD Project: {project-name}

    Tech stack: {language} / {framework} / {database}

    Domains:
      users (4 flows, 2 schemas)
      orders (3 flows, 3 schemas)
      notifications (2 flows, 0 schemas)

    Schemas: user, session, order, order_item, payment
    Total flows: 9

    Files created:
      ddd-project.json
      specs/system.yaml
      specs/architecture.yaml
      specs/config.yaml
      specs/shared/errors.yaml
      specs/shared/types.yaml
      specs/schemas/_base.yaml
      specs/schemas/user.yaml
      ...
      specs/domains/users/domain.yaml
      specs/domains/users/flows/user-register.yaml
      ...

    Event wiring:
      UserRegistered: users → notifications
      OrderCreated: orders → notifications
      PaymentProcessed: orders → (no consumer — warning)

    Warnings:
      - PaymentProcessed event has no consumer
      - orders/refund-order: complex switch/case simplified to decision chain

    Next steps:
      1. Open the project in DDD Tool to visualize and review
      2. Refine any flows that were simplified during extraction
      3. Run /ddd-implement --all to verify round-trip (generated code should match original)
    ```

## Node Type Reference

When creating nodes during extraction, use the correct spec structure for each type:

| Type | Required Spec Fields | Connections |
|------|---------------------|-------------|
| `trigger` | `event`, `source` | Single output |
| `input` | `fields` (array of `{name, type, required?}`), `validation` | `sourceHandle: "valid"` + `sourceHandle: "invalid"` |
| `process` | `action`, `service` | Single output |
| `decision` | `condition`, `trueLabel`, `falseLabel` | `sourceHandle: "true"` + `sourceHandle: "false"` |
| `terminal` | `outcome`; also `status` (HTTP code), `body` (response shape) | None (endpoint) |
| `data_store` | `operation` (create/read/update/delete), `model`; also `pagination`, `sort` for reads | `sourceHandle: "success"` + `sourceHandle: "error"` |
| `service_call` | `method` (GET/POST/PUT/PATCH/DELETE), `url`; also `error_mapping` | `sourceHandle: "success"` + `sourceHandle: "error"` |
| `event` | `direction` (emit/consume), `event_name` | Single output |
| `loop` | `collection`, `iterator` | `sourceHandle: "body"` + `sourceHandle: "done"` |
| `parallel` | `branches` (2+ items), `join` (all/any/n_of) | `sourceHandle: "branch-0"`, `"branch-1"`, ... + `sourceHandle: "done"` |
| `sub_flow` | `flow_ref` (domain/flow-id format) | Single output |
| `llm_call` | `model`, `prompt_template` | Single output |
| `agent_loop` | `model`, `system_prompt`, `tools` (with 1+ terminal tool), `max_iterations` | Single output |
| `guardrail` | `position` (input/output), `checks` | Single output |
| `human_gate` | `notification_channels`, `approval_options`, `timeout` | Single output |
| `orchestrator` | `strategy`, `agents` (2+ items) | Single output |
| `smart_router` | `rules` | Multiple outputs (one per route name) |
| `handoff` | `mode`, `target` | Single output |
| `agent_group` | `members` (2+ items) | Single output |

$ARGUMENTS
