# ForgeLink Agent Contract

The repository is the durable coordination surface for ForgeLink. State that matters —
authority, intent, decisions, evidence, and history — lives in versioned files, not in
conversation (`governance/invariants.json`, binding; weakening one requires operator
approval). Read every `AGENTS.md` from the root down to the file you touch.

## Scopes and ownership

Ownership and writable scopes are declared in
[`governance/owners.json`](governance/owners.json). Work is captured as records under
`work/`, proven by `evidence/runs/`, and reconciled through `audits/`. Nested
contracts (e.g. under `work/`) refine this root contract but cannot weaken it.

## Governed with RepoPact

ForgeLink is governed with [RepoPact](https://github.com/ForgeWireLabs/repopact),
consumed as a pinned upstream package (`3.0.2`, pinned in
`requirements-repopact.txt`; decision 0015). Validate with `python .local/validate_system.py` (it runs `repopact validate`
plus ForgeLink's local checks). Run `pip install -r requirements-repopact.txt` on a
fresh clone first. Derived artifacts (`audits/reports/dashboard.md`) are generated,
never hand-edited.

`schemas/` stay in-repo — RepoPact validates against this repository's own contracts.
There are no vendored validator patches; the preflight guard is an upstream opt-in
enabled via `governance/owners.json`. See
[`scripts/LOCAL_EXTENSIONS.md`](scripts/LOCAL_EXTENSIONS.md) for the history and the
current model.

<!-- BEGIN SHARED AGENT SELF-AUDIT v1 -->
## Mandatory pre-completion adversarial self-audit

Before claiming completion or requesting review, inspect the full task-scoped change against an explicit review base: committed branch diff, staged and unstaged changes, and relevant untracked files. Record base/HEAD and preserve unrelated user changes. A bare `git diff` is not the whole candidate.

Look for concrete correctness and edge-case defects, concurrency/races, fail-closed behavior, API/schema compatibility, security and authority boundaries, durability, resource leaks/cleanup, missing positive and negative tests, and unnecessary complexity or out-of-scope edits. Tie each finding to a location and credible failure scenario; do not invent stylistic defects or churn working code.

Repair confirmed defects only within authorized scope, rerun affected checks, and reinspect remediation. Use at most two repair/re-review cycles by default; if blocked, report `INCOMPLETE` or `FAIL` instead of looping or weakening tests/invariants. Escalate changes requiring new authority.

Pre-existing failures are not waived by showing they also occur on the baseline. Separate cause attribution from resolution: repair the confirmed root cause when authorized, or create/link an owned, actionable remediation work item with reproduction, evidence, and a validation gate. Preserve failures and keep project-level health accurately red or incomplete until resolved. Never use permanent skips, false evidence, or weakened assertions to manufacture green results.

Handoff must state `Self-Audit: PASS|INCOMPLETE|FAIL`, reviewed revision and scope, concrete findings/fixes (or no confirmed findings), actual checks/results, unrun checks, and residual risks. PASS means review completed with no known in-scope blockers, not proof of defect freedom. Self-review is neither independent approval nor authorization to merge, deploy, release, publish, or perform destructive operations.
<!-- END SHARED AGENT SELF-AUDIT v1 -->
