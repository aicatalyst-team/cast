# PoC Plan: Cast

## Project Classification
- **Type:** llm-app
- **Key Technologies:** Node.js 22, TypeScript, Express 5, Preact, Vite, pnpm, better-sqlite3, Claude Agent SDK, MCP
- **ODH Relevance:** Demonstrates multi-user agent orchestration with config-driven access control on OpenShift AI; validates agentic-ai deployment patterns

## PoC Objectives
1. Containerize the Cast server (API + web UI bundle) as a single UBI-based image
2. Deploy on OpenShift and verify the admin dashboard is accessible
3. Validate that the server starts, serves the web UI, and responds to API health checks
4. Demonstrate the agent configuration and admin interface without requiring container-in-container

## Infrastructure Requirements
- **Resource Profile:** medium (1Gi RAM, 500m CPU)
- **GPU Required:** No
- **Persistent Storage:** None for PoC (SQLite in-memory acceptable)
- **Sidecar Containers:** None
- **LLM API:** Not required for PoC (server starts without agent API keys)

## Deployment Model
- **Type:** deployment
- **Listens on Port:** true (port 5051 combined API + web UI)
- **Long Running:** true

## Test Scenarios

### Scenario 1: health-check
- **Description:** Verify the Cast server starts and responds to HTTP requests
- **Type:** http
- **Input:** GET /admin/
- **Expected:** Returns 200 OK with HTML content
- **Timeout:** 60 seconds

### Scenario 2: api-health
- **Description:** Verify the API server is reachable via the web proxy
- **Type:** http
- **Input:** GET /api/agents
- **Expected:** Returns 200 with JSON response (empty array for fresh install)
- **Timeout:** 30 seconds

### Scenario 3: static-assets
- **Description:** Verify static web UI assets are served correctly
- **Type:** http
- **Input:** GET /admin/assets/ (any JS/CSS file from the build)
- **Expected:** Returns 200 with appropriate content type
- **Timeout:** 15 seconds

## Dockerfile Considerations
- Use `registry.access.redhat.com/ubi9/nodejs-22` as base
- pnpm monorepo needs pnpm installed globally
- Bundle server with `pnpm bundle` (produces dist/index.js)
- Build web-ui with `pnpm --filter @getcast/web-ui build`
- Native addon better-sqlite3 needs build tools (gcc, python3, make)
- Combined single-container approach: API server serves the bundled web UI
- Ensure port 5051 is exposed (or configure for 8080)

## Deployment Considerations
- Single Deployment with 1 replica
- Service on port 8080 (redirect from default 5051)
- Set CAST_PORT and PORT env vars to configure listening ports
- CAST_AGENTS_DIR and CAST_CONFIG_DIR for data directories
- No secrets required for basic PoC (agents won't be created without API keys)
