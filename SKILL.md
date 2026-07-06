---
name: writing-tools
description: Invoke ONLY when the user types the explicit slash command `/writing-tools`. This skill helps the user either write new content from scratch or clean up an existing draft, using Roy Peter Clark's 51 writing tools. The user has deliberately chosen explicit invocation and does NOT want this skill auto-triggered for general writing, editing, or proofreading requests. If the user asks about writing without typing `/writing-tools`, do not load this skill.
---

# writing-tools

Help the user write new content or edit existing content using a curated subset of Roy Peter Clark's 51 writing tools. Only the tools that actually fit the kind of content get applied.

## Hard rules (apply to everything this skill produces)

1. **Never use em dashes or en dashes as punctuation in any output.** (The em dash is the long horizontal line roughly three hyphens wide. The en dash is shorter, roughly two hyphens wide. Both are banned.) If the user's original draft contains either character, replace them during the rewrite. Substitute a comma, semicolon, parentheses, or period, chosen by the rhythm of the sentence. This rule covers drafts, rewrites, the summary of changes, and any chat message sent while this skill is running. Regular hyphens (the single character on the keyboard) inside compound words like "short-form" or "long-form" are fine.
2. Every recommendation and revision should tie back to one of Clark's 51 tools. Use `tools-index.md` as the canonical list of tool numbers, principles, and when to reach for each.
3. Stay general-purpose. Do not defer to other skills (for example, velacare-editor-in-chief or write-pet-health-copy). The user will pick the right skill themselves.

## How to route the request

When invoked, look at what came along with the slash command and branch:

- **Nothing passed.** Ask the user: "Writing something new or cleaning up an existing draft?"
- **Pasted text.** Assume it is a draft to edit. If the text reads more like a brief or topic prompt than a draft, confirm with: "Is this a draft you'd like me to edit, or a brief for me to write from?"
- **A file path.** Read the file and assume edit mode.
- **A topic or brief** (e.g. "write a landing page for X"). Assume write mode.

## Ask for content type (do not skip this step)

This step is critical. It is how the skill knows which subset of tools to apply. Present six options and ask the user to pick one:

1. Email (internal or external)
2. Memo, report, or internal doc
3. Slide notes or presentation copy
4. Short-form copy (headlines, subject lines, CTAs, button text)
5. Product or landing page copy
6. Explainer, guide, article, or blog post

Once the user picks, look up the matching tool subset in `content-type-map.md`. Load only those tool numbers. For deeper context on any tool, consult `tools-index.md`.

## Route by short-form versus long-form

The content type also decides whether to plan before drafting.

**Short-form content types: 1 (Email), 4 (Short-form copy), 5 (Product or landing page copy).**

- In write mode: go straight to draft. Skip the outline step.
- In edit mode: go straight to a clean rewrite.

**Long-form content types: 2 (Memo or report), 3 (Slide notes), 6 (Explainer or guide).**

- In write mode: first ask the user for a mission statement (Tool #36). Prompt with something like: "In one sentence: what is this piece about, and what should the reader take away?" Once they answer, draft an outline using Tool #24 (Name the Big Parts). Show the outline, ask for changes, and wait for approval. Then draft the full piece.
- In edit mode: go straight to a clean rewrite.

## Output format

**Write mode output**

1. The draft itself.
2. A short section titled "How the tools shaped this." List the 3 to 5 tools that most drove the choices, one line each. Example line: "Tool #2 (Use Strong Verbs): picked 'seize' and 'plant' over 'is' and 'make' to make the action concrete." Keep it brief.

**Edit mode output**

1. A clean rewrite of the full draft.
2. A short section titled "Top changes." List only the 2 to 3 biggest changes. Tag each one with its tool number and name. Example: "Cut the opening clause. Tool #1 (Branch to the Right): the subject and verb were buried 14 words in." Do not cite tools for micro-edits like swapping a single weak word. Those go unexplained.

## Guidance while drafting or editing

Read the source draft (if editing) or the brief (if writing) carefully before applying tools. Tools are diagnostic aids, not a checklist. Only apply a tool when it actually improves the piece.

When two tools pull in opposite directions (for example, Tool #26 "Fear Not the Long Sentence" versus Tool #34 "Cut Big, Then Small"), use the content type and the piece's rhythm to decide. Short-form favors cuts; explainers can absorb longer rhythm.

If the user specifies a focus area (for example, "make this tighter" or "focus on verbs"), honor that by weighting those tools more heavily, but still run the full curated subset as a base.

Keep voice consistent with what the user has written or asked for. Do not impose a voice.

If the draft is long enough that it will not fit comfortably in one response, offer to handle it in sections, working top to bottom, and keep the section breaks at natural boundaries.

## Quick reference: the six content types at a glance

| # | Content type | Short or long | Tools loaded from content-type-map.md |
|---|---|---|---|
| 1 | Email | Short | #1, #2, #3, #11, #34, #38, #39 |
| 2 | Memo, report, internal doc | Long | #9, #12, #24, #30, #34, #36, #42 |
| 3 | Slide notes, presentation copy | Long | #2, #4, #12, #25, #38 |
| 4 | Short-form copy | Short | #2, #4, #8, #14, #16, #25, #38 |
| 5 | Product or landing page copy | Short | #1, #2, #9, #13, #25, #38 |
| 6 | Explainer, guide, article, blog | Long | #9, #12, #13, #18, #23, #24, #30, #36, #42 |
