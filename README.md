# Hunt3d

> **An AI research partner for security researchers.** Turn authorized investigations into evidence-backed findings you can reproduce, review, and report.

Hunt3d is an early-stage concept for an evidence-first security research workspace for bug bounty hunters and independent penetration testers. Instead of producing a pile of scanner alerts, Hunt3d is designed to preserve investigation context, connect claims to evidence, and help researchers produce reproducible reports.

> **Status:** concept / prototype scaffold. This repository contains the product brief and a Remotion motion-graphic promo. It is not a working pentesting engine and does not execute security tests.

## Product thesis

Security tooling can produce plenty of output. Researchers still need to decide what matters, validate behavior, preserve proof, avoid repeated work, and write a report someone else can reproduce. Hunt3d focuses on that investigation workflow.

### Product principles

- **Evidence before claims.** Every finding should link to observable evidence.
- **Human-owned decisions.** AI suggestions are not automatically confirmed vulnerabilities.
- **Scope is a hard boundary.** Execution must be restricted to explicitly authorized targets.
- **Research should persist.** Hypotheses, attempts, outcomes, and notes should survive across sessions.
- **Local-first by default.** Sensitive request/response artifacts deserve deliberate handling and clear retention controls.

## Intended workflow

1. Create a project and define the authorized scope.
2. Start an investigation and record a hypothesis.
3. Attach request/response evidence and notes.
4. Ask the assistant to organize evidence and propose a bounded next step.
5. Review the verification status and evidence trail.
6. Export a reproducible Markdown report.

## Proposed architecture

- **Web:** Next.js + TypeScript
- **UI:** Tailwind CSS + shadcn/ui
- **Validation:** Zod
- **Database:** PostgreSQL + Drizzle ORM for a hosted product; SQLite is viable for a strictly local prototype
- **Execution:** separate worker process with persistent jobs and bounded runs
- **Agent:** one orchestrator with typed tools and explicit state transitions
- **Evidence:** structured metadata in the database; larger artifacts in controlled file/object storage
- **Isolation:** sandboxed tools, restrictive egress, timeouts, resource limits, and audit events

Start as a modular monolith plus one worker. Avoid a distributed agent swarm until benchmarks show a clear advantage.

## Core domains

- **Projects & scope:** authorized assets, exclusions, ownership, and project settings.
- **Investigations:** research sessions, hypotheses, notes, and execution timeline.
- **Runs & approvals:** queued work, bounded agent steps, cancellations, and human approval gates.
- **Evidence:** immutable artifacts, hashes, provenance, annotations, and controlled exports.
- **Findings:** severity, confidence, verification state, remediation, and linked evidence.
- **Reports:** versioned report snapshots built from reviewed findings.
- **Audit:** scope changes, approvals, tool executions, exports, and permission changes.

## What is intentionally out of scope for this scaffold

- Automated scanning or exploitation of arbitrary internet targets
- Unrestricted shell access for an LLM
- Automatic bug bounty report submission
- Claims of confirmed vulnerabilities without evidence
- Multi-agent orchestration, enterprise SSO, billing, and cloud-scale deployment

## Promo video

The Remotion composition is 40 seconds, 16:9, 30 fps, 1920×1080. It presents the product thesis, investigation flow, evidence model, scope controls, and closing message.

### Run the Remotion project

Requires Node.js 20+.

```bash
npm install
npm run studio
```

Render the MP4:

```bash
npm run render
```

The composition ID is `Hunt3dPromo`.

## Roadmap

### Phase 1 — Research workspace
- Projects and explicit scope rules
- Investigations and hypotheses
- Evidence capture and provenance
- Finding review and Markdown export

### Phase 2 — Bounded assistant
- Structured hypothesis generation
- Typed, allowlisted tool contracts
- Persistent run lifecycle and cancellation
- Human approval for higher-risk actions

### Phase 3 — Validation
- Lab-based benchmark set
- Confirmed-finding precision and false-positive measurement
- Design-partner pilots with independent researchers
- Usage and cost instrumentation

## Safety model

Hunt3d is intended only for systems the user owns or is explicitly authorized to test. A future execution engine must enforce scope and action policy in code, not rely on a prompt. It should use deny-by-default target policies, controlled egress, rate limits, process isolation, budget limits, human approvals, and auditable actions.

## License

MIT. See [LICENSE](LICENSE).
