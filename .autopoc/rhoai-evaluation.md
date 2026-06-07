# RHOAI Evaluation: Cast

## Scores (0-20 scale)

| Dimension | Score | Rationale |
|-----------|-------|-----------|
| Audience Value | 16 | Multi-user agent orchestration is highly relevant to enterprise AI platform teams |
| Strategic Alignment | 14 | Aligns with agentic AI and MCP strategies; uses Claude Agent SDK |
| Strategy Fit | 14 | Fits agentic-ai strategy area; demonstrates agent containment and routing |
| Platform Leverage | 12 | Self-hosted architecture maps well to OpenShift deployment model |
| Demo Potential | 14 | Web dashboard with real-time agent interaction is visually compelling |

**Impact Score:** (16 + 14 + 14 + 12 + 14) / 5 = **14.0 / 20**

## Feasibility

| Dimension | Score | Rationale |
|-----------|-------|-----------|
| Container Readiness | 7 | Has existing Dockerfile for agent-runner; pnpm monorepo builds cleanly |
| Dependency Profile | 6 | Native addon (better-sqlite3) and pnpm workspace complexity |
| Reproduction Confidence | 7 | Clear build instructions in README; pnpm start bootstraps everything |
| Complexity Sweet Spot | 7 | Single server + web UI is deployable; agent containers are optional for PoC |

**Feasibility Score:** (7 + 6 + 7 + 7) / 4 = **6.75 / 10**

## Relationship to Red Hat AI
- **Type:** Adjacent
- **Strategy Areas:** agentic-ai, developer-experience
- **Capability Labels:** agent-runtime, mcp, ai-hub

## Strengths
- MIT license
- Clean architecture with clear separation of concerns
- Config-driven access control (not prompt-based)
- Multi-user, multi-agent design

## Risks
- Agent-runner requires container-in-container (Docker/Apple Container)
- Anthropic-specific (Claude Agent SDK dependency)
- Alpha status software
