# DDD Sync

Synchronize the DDD project specs with the current implementation state. This updates the DDD project files so the DDD Tool reflects what's actually implemented.

## Instructions

1. **Find the DDD project**: Look for `ddd-project.json` in the current directory or parent directories.

2. **Scan the implementation**:
   - Read `.ddd/mapping.yaml` for currently tracked flow mappings
   - For each mapped flow, check if the implementation files still exist
   - Look for any new source files that aren't mapped yet

3. **Update mapping.yaml**:
   - For each implemented flow, compute the current `specHash` from the flow YAML
   - Update the `files` list with all source files that are part of the implementation
   - Update `implementedAt` timestamp if files have changed
   - Remove entries for flows that no longer have implementation files

4. **Detect new patterns** (if `--discover` or `--full` flag):
   - Scan `src/` for route handlers, services, models that don't have corresponding flow specs
   - Suggest which DDD flows should be created for untracked code
   - If the user agrees, create new flow YAML specs under `specs/domains/`

5. **Fix drift** (if `--fix-drift` or `--full` flag):
   - For each flow where the spec has changed since implementation (specHash mismatch), re-implement:
     - Read the updated flow spec
     - Read the existing implementation files from mapping
     - Update the implementation to match the new spec
     - Run tests and fix until passing
     - Update mapping.yaml with new specHash and timestamp

6. **Report**:
   - Show a summary of what was synced:
     - Flows with up-to-date specs
     - Flows with spec drift (spec changed since implementation)
     - Flows with missing implementation
     - (If --discover or --full) Untracked code that should become flows
     - (If --fix-drift or --full) Flows that were re-implemented

## Usage

The user will say something like:
- `/ddd-sync` — sync mapping.yaml with current implementation state
- `/ddd-sync --discover` — also discover untracked code and suggest new flow specs
- `/ddd-sync --fix-drift` — re-implement flows where specs have drifted from implementation
- `/ddd-sync --full` — do all of the above: sync mapping, discover untracked code, and fix drifted flows

$ARGUMENTS
