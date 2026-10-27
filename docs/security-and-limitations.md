# Security, redactions, and limitations

## Public export policy

The workflows in this repository are **public portfolio examples**, derived from historical exports, not a production backup or a functional deployment package.

Changes to the public copies:

- Entire workflow marked **inactive**.
- n8n workflow IDs, version IDs, instance identifiers, webhook identifiers, and original node identifiers removed/replaced.
- Credentials references and their internal IDs/names removed.
- Personal SMTP sender/recipient addresses replaced with `example.com` addresses.
- Local Windows repository/workspace paths replaced or omitted.
- Historical task identity replaced with `PORTFOLIO-DEMO-001`, expected agent branch changed to a dummy example.
- `run_mode` forcibly set to `PREVIEW_ONLY` and `approved_for_execution` to `false` in the public Task Spec.
- The **HTTP POST Worker Task Action** node replaced with an n8n **No Operation** node; its original mutating request payload cannot be sent from the public export.
- The **local Execute Command quota-probe node** replaced with a **No Operation** node; the public export cannot invoke a local shell command.
- Original stage specifications and read-only status normalization are retained for educational inspection.

> These modifications intentionally make the public orchestrator **non-operational**. Import the JSON to review its layout and Code nodes; do not activate or attempt production use. A working deployment requires separate engineering, live credential configuration, independent security review, and human approval.

## Known limitations

1. **Custom Worker not included.** API contract, Task State persistence, permission enforcement, worktree control, agent jobs, and test execution require a separate Worker project.
2. **Quota probe not included.** The original workflow called an external local JavaScript tool. Only the n8n decision logic is visible here.
3. **No deployment configuration.** There is no Docker Compose deployment, infrastructure provisioning, or packaged credentials.
4. **No production execution logs.** Historic completion/test status is supported by project documentation; screenshots, telemetry, timing metrics, and external verification are not provided here.
5. **Historical task is closed.** The original `DD-GAME-13-003` and its archived branch cannot be reused for a new task. Each real execution requires a fresh approved task ID, spec, baseline, Worker state, and manual authorization.
6. **SMTP behavior differs by trigger.** The Error Trigger does not cover manual n8n runs in the same way as automatic production executions.

## Before publishing your own screenshots and exports

- Never publish `.env`, SMTP passwords, OAuth secrets, API keys, personal email addresses, authentication headers, or private task/log payloads.
- Inspect `Code` nodes, Sticky Notes, URLs, commands, node credentials, metadata, and pinned execution data, not just the n8n credential interface.
- Screenshot the **workflow canvas** rather than HTTP responses containing headers or private execution payloads; blur paths and personal addresses.
- If sensitive material was already pushed publicly, deleting a file later does **not** reliably remove it from Git history; revoke/rotate affected secrets and address repository history.
- Keep this repository separate from the application's full source and from the private Worker configuration.
