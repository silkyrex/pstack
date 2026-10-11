# Upstream constraints

Use this source when an external API, service limit, dependency change, or deprecation could explain the target code.

## How to search it

1. Identify the dependency or service and the version relevant to the target commit. Read its lockfile, manifest, API version, or recorded invocation. Keep the currently installed version separate from the historical version.
2. Use available web tools or documentation readers to find official, version-matched documentation, tagged source, and release notes. Start with any exact official reference already supplied or verified. Treat latest-version documentation as a separate source.
3. Read the contract or release entry that bears on the code. Record the supported behavior, limit, breaking change, or deprecation and its effective version or date.
4. Cross-reference the introducing commit or PR for the author's stated reason. Send that lead to the source control investigator. Documentation establishes an external constraint; it does not by itself establish why the author chose this implementation.

If the historical documentation or version cannot be verified, report the gap. Do not substitute current documentation silently. Follow applicable source preferences and access boundaries. This investigation does not upgrade dependencies, change settings, or expand access.

## What good evidence looks like here

- An official versioned contract that matches the relevant API or dependency.
- A release note naming a breaking change before the compatibility code appeared.
- A tagged upstream implementation that confirms a documented limitation.
- A PR explanation linking the local change to that exact upstream constraint.

## What to return

For each relevant item, return its title, official URL, dependency or API version, publication or effective date when available, and the specific supporting passage or symbol. Record when you read it and whether it describes historical or current behavior.

State which fact is documented, which connection to the local code is inferred, and what remains unverified. Preserve conflicting versions as separate findings.
