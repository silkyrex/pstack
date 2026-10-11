# Code Archaeology (git + in-repo)

## What this source contains

- Commit history (messages, dates, authors, diffs)
- PR descriptions, review comments, and discussion threads (via `gh`)
- Inline code comments, TODOs, FIXMEs, deprecation notes
- ADRs (architectural decision records) if the repo keeps them
- Tests. Names and assertions often encode the edge cases that motivated a change
- Related files modified in the same commits (co-change signal)
- CHANGELOG entries, release notes in the repo
- Issue/ticket IDs mentioned in commit messages and PR bodies

The most trustworthy source, tied directly to the code, and the most complete. Everything that went through the repo should be here.

## How to search it

Expand the seed commit list:

```bash
# Full history of the file through renames
git log --follow --oneline -- <file>

# Pickaxe: commits that added or removed this exact text
git log -S '<exact_string_from_code>' -- <file>

# Or for patterns:
git log -G '<regex>' -- <file>

# Who wrote each line and when
git blame -L <start>,<end> <file>

# The full diff of a specific commit
git show <hash>

# Commits between two points affecting this file
git log <old>..<new> -p -- <file>
```

For each substantive commit, pull the PR context:

```bash
# Find the PR number from the merge commit or branch
git log -1 --format=%B <hash>

# Full PR context: body, review comments, linked issues
gh pr view <number> --json title,body,author,createdAt,mergedAt,labels,closingIssuesReferences,comments,reviews,files

# The --json reviews and comments fields are where the real signal is
```

Look for out-of-band docs:

```bash
# ADRs often live in docs/adr/ or similar
rg -l -i 'architecture.decision' --glob '*.md'

# TODOs and FIXMEs near the target
rg -n -C2 '(TODO|FIXME|HACK|XXX|NOTE)' <target_file>

# Related tests. Names often encode the "why"
rg -l '<symbol>' --glob '*test*'
```

### Chat evidence

Follow the transcript-search and scope instructions in [`recall`](../../../recall/SKILL.md). Pin the workspace, topic, and time window. Reuse that search section only; the full recall workflow calls `why` and would repeat this investigation. Report a missing skill or inaccessible transcript as a gap.

Return the original user instruction or correction with its session identifier, timestamp, and message location. Distinguish an agent's proposal or completion claim from its observed tool actions. Later accepted decisions can supersede a chat; send cross-source references to the owning investigator.

### Configuration evidence

Read the installed [`setup-pstack`](../../../setup-pstack/SKILL.md) and its app-selection reference, if present. Follow applicable user policy to select the current app's settings. Keep model choices and permissions separate.

Reuse an existing verification skill for the target app. For example, an installed `verify-pstack-app-settings` owns its probe and evidence format. Read its instructions and already available results. Run a probe only within the task's existing authorization. If no matching skill exists, record the gap without building one.

Tie each result to its actual invocation, app version, source version, tested action, and timestamp. A result from another version or scope is historical evidence, not proof of the current state. Distinguish configured, installed, loaded, and exercised. A readable file or a passing CLI probe does not prove GUI adoption or actual model delegation. Keep each verifier's stated limits with its result. Read relevant non-secret settings only.

### Historical build and test failures

Use the target commit to locate check runs, including their attempts:

```bash
gh run list --repo <owner/repo> --commit <sha> --limit 20 --json databaseId,headSha,attempt,workflowName,event,status,conclusion,createdAt,url
gh run view <run-id> --repo <owner/repo> --attempt <attempt> --json headSha,attempt,event,status,conclusion,createdAt,url,jobs
gh run view <run-id> --repo <owner/repo> --attempt <attempt> --log-failed
```

For pull requests, distinguish the source commit from the workflow's tested merge commit. Record both when they differ. Narrow to the relevant failed job and retain its run URL, commit, attempt, timestamp, and error excerpt. A failed run with no job results does not establish a test failure. Unavailable logs or missing access are gaps; a later successful attempt does not erase an earlier failure.

Use PR discussion or commit messages to establish why a failure motivated a change. The log alone proves the failure. This investigation does not retry jobs or change code. [`babysit`](../../../poteto-mode/playbooks/babysit.md) and [`shipping`](../../../poteto-mode/playbooks/shipping.md) own remediation and delivery under the user's authorization.

## What good evidence looks like here

- A PR description that explains the problem being solved, not just the change ("This fixes the pagination bug that caused X")
- A long review thread where alternatives were debated
- An inline comment near the target line that explains a non-obvious constraint
- A test named `test_handles_edge_case_when_X` that reveals an edge case motivating the code
- A commit message that references a ticket or incident ID
- A CHANGELOG entry that summarizes the user-visible rationale

## Common pitfalls

- **Squash-merge flatlands.** If the repo squashes PRs, individual commits in the branch history are lost. Fall back to PR body and comments.
- **Misleading commit messages.** "Small refactor" sometimes hides an intentional behavior change. Look at the diff, not the message.
- **Cargo-culted patterns.** The author may have copied a pattern without understanding why. Check if the pattern originated earlier in the codebase and investigate *that* commit.
- **Bot commits and auto-merges.** Dependabot, Renovate, and automated backports usually don't carry motivation. Skip them when trying to find intent.
- **Treating code as evidence of intent.** The code itself isn't evidence for why it exists. Evidence comes from commit messages, PRs, comments, tests, docs. Don't cite "the function is named X" as evidence of intent.

## What to return

Every commit/PR/comment that bears on the question, with:
- The exact text (quoted)
- The hash / PR number / file:line
- Author and date
- Whether it's direct (explicitly addresses the question) or circumstantial

For chat, configuration, and check-run evidence, include the searched scope, original source location, source version or commit, and verification limits. Keep unavailable evidence separate from an empty search result.
