# Notion Docs

## What this source contains

- PRDs (product requirement documents)
- Technical specs and RFCs
- Architectural decision records (ADRs)
- Meeting notes from design reviews
- Team pages with domain context
- Postmortems from incidents
- Runbooks that may explain defensive code
- Strategy documents that set priorities

Notion is where "why" often lives in long-form before it becomes code. A significant feature usually has a doc.

## How to search it

Use the available Notion search and fetch tools. Tool names below are examples; resolve their equivalents from the current tool catalog.

For a personal goal, standard, preference, or prior decision, follow the context directory and authority rules named in applicable user instructions. Reuse exact sources already verified in this session. Start with the directory and one relevant source; expand only for a material gap. Keep those policies and their source documents in their existing homes.

Record acceptance, effective scope, and explicit superseding decisions. Distinguish a current instruction from a proposal, draft, or historical snapshot. A recent edit alone does not establish authority or permission. Surface unresolved material conflicts with both sources. This investigation reads evidence; it does not rewrite decisions or create a second task system.

1. **Keyword searches with `notion-search`.** Try:
   - The feature name
   - Key symbols / class names from the target code
   - Author handles (design docs are often authored before the code lands)
   - Error strings or user-visible terms
   - Time-bounded queries if you know when the code shipped
2. **Fetch candidate pages with `notion-fetch`.** Read the full content, not the preview. Rationale is often buried mid-document.
3. **Follow backlinks and child pages.** Design docs often have sub-pages for alternatives considered, appendices, or implementation notes.
4. **Check related databases.** `notion-query-data-sources` and `notion-query-meeting-notes` can surface meeting notes that discussed the decision.
5. **Search author-specific spaces.** If the PR author has a personal notebook (common at some companies), it may hold exploratory thinking that preceded the code.

## What good evidence looks like here

- A PRD with a "Problem statement" or "Motivation" section that matches the target code's purpose
- An "Alternatives considered" or "Rejected approaches" section
- A postmortem that names the target code as the fix for a specific incident
- Meeting notes that record "we decided X because Y" and tie to the same author/date range as the PR
- An ADR template filled out non-trivially (status, context, decision, consequences)

## Common pitfalls

- **Outdated docs.** Specs are often written before implementation and not updated. The doc may describe a plan that changed. Cross-check against the actual PR.
- **Doc vs. reality drift.** A spec may say "we'll do X" but the code actually does Y. Flag the divergence. The synthesizer will surface the contradiction.
- **Boilerplate templates.** Some orgs require a "Why" section that gets filled with fluff. Look for specificity.
- **Unlinked docs.** The most relevant doc may not be linked from anywhere. Broad keyword searches help.
- **Multiple drafts.** Check acceptance, effective dates, and explicit superseding decisions. A finalized document or a recent edit may still be superseded. Follow the applicable authority rules rather than choosing by recency alone.
- **Access-restricted pages.** If you can't access a page, note it as a gap.

## What to return

For each relevant doc:
- Title and URL
- Authors and last-updated date
- The motivation text (verbatim quote), with page/section location
- Relevant linked pages (so the synthesizer can cite them)
- Whether the doc was accepted, proposed, draft, or superseded; its effective scope and any unresolved authority gap
