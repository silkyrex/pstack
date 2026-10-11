# Source playbooks

The why skill assigns one investigator per available evidence category, each reading its matching playbook below. The playbooks cover local readers, CLIs, web tools, and common MCPs. Adapt them for an available tool in the same category, subject to the user's delegation rules.

| Category | Playbook | Example evidence access |
|---|---|---|
| Source control history and related local evidence | [`code-archaeology.md`](./sources/code-archaeology.md) | git, `gh`, available local readers |
| Issue / ticket tracker | [`linear.md`](./sources/linear.md) | Linear (adapt for Jira, GitHub Issues, Plane, Shortcut) |
| Long-form documents | [`notion.md`](./sources/notion.md) | Notion (adapt for Confluence, Google Docs, Coda) |
| Real-time team chat | [`slack.md`](./sources/slack.md) | Slack (adapt for Discord, Microsoft Teams, Mattermost) |
| Infrastructure observability | [`datadog.md`](./sources/datadog.md) | Datadog (adapt for New Relic, Honeycomb, Grafana, Splunk) |
| Error / exception tracking | [`sentry.md`](./sources/sentry.md) | Sentry (adapt for Rollbar, Bugsnag, Airbrake) |
| Product analytics warehouse | [`databricks.md`](./sources/databricks.md) | Databricks SQL (adapt for Snowflake, BigQuery, ClickHouse, dbt) |
| Upstream constraints, when applicable | [`upstream-constraints.md`](./sources/upstream-constraints.md) | Available web tools or official documentation readers |

Reuse existing owners:

- Chat evidence follows the transcript-search and scope instructions in [`recall`](../../recall/SKILL.md). Use that section only; invoking its full workflow would call `why` again.
- Configuration evidence follows the installed [`setup-pstack`](../../setup-pstack/SKILL.md) and any existing verification skill for the target app. `code-archaeology.md` explains how to read their evidence and limits.
- Historical check failures stay in `code-archaeology.md`. Existing [`babysit`](../../poteto-mode/playbooks/babysit.md) and [`shipping`](../../poteto-mode/playbooks/shipping.md) own remediation and delivery.
- Personal decisions follow `notion.md` and the authority rules or context directory in applicable user instructions. Keep those policies in their existing homes.

Cross-cutting:

- [`incident-postmortem.md`](./sources/incident-postmortem.md). Add this if the target code looks defensive (null checks, retry, timeout, rate limit, feature flag, egress guard, OOM handler).
