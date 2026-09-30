---
name: questionnaire-design
description: "Design, build, edit, preview, or validate online questionnaires, especially in WJX/问卷星. Use this skill to enforce respondent routing, question-type consistency, required/optional states, multi-select limits, draft-save checks, and self-testing of every branch before delivery or publication."
---

# Questionnaire Design

Use this skill whenever the request involves designing, importing, editing, previewing, saving, publishing, or checking an online questionnaire. The goal is a questionnaire that is logically complete on the first delivery, with evidence from a self-check rather than an assumption that a batch edit worked.

## Operating rules

1. Preserve the user's title, research scope, wording decisions, and sample restrictions. Do not invent age restrictions, demographic items, answer data, or publication permission.
2. Separate content review from platform operations. First write a compact question inventory and routing table; then edit the platform; then re-read the saved result.
3. Treat every routing operation as untrusted until each affected question is checked individually. Batch application can silently skip intermediate questions.
4. Use the platform's current state after each meaningful action. Do not rely on stale screen text or a previous preview.
5. Save the draft after changes. Do not publish, generate a public collection link, or start collection unless the user explicitly authorizes that final external action.
6. If a required platform control is unavailable or ambiguous, report the exact uncertainty instead of claiming completion.

## Required preflight inventory

Before editing, record:

- title and introduction;
- question number, label, type, options, and required/optional state;
- which question is the termination screen;
- every condition and its target range;
- multi-select maximums;
- whether the current request is draft-only, preview-only, or publication-authorized.

If the questionnaire is based on a previously corrected design, carry forward these known invariants unless the user explicitly changes them.

## Canonical channel-routing pattern

For a questionnaire comparing online and store experiences, use a mutually exclusive single-choice channel question:

| Answer | Route |
|---|---|
| No purchase experience | End with a clear thank-you message |
| Online only | Basic questions → online block → overall questions → optional feedback/contact |
| Store only | Basic questions → store block → overall questions → optional feedback/contact |
| Both online and store | Basic questions → online block → store block → comparison/integration block → overall questions → optional feedback/contact |

The online block must be visible only to online-experienced respondents. The store block must be visible only to store-experienced respondents. Direct online-versus-store comparison and channel-integration questions must be visible only to respondents with both experiences. General improvement, purchase intention, recommendation, survey feedback, and optional interview recruitment may be shown to every valid purchaser.

Never implement the three channel answers as a checkbox question. Never show a comparison question to a respondent who has only used one channel.

## Specific checks learned from prior failures

- Check the termination question separately from the channel question. A non-purchaser should end; age alone should not end the questionnaire unless the user explicitly requests it or an approved research-ethics rule requires it.
- If the user says under-18 respondents should continue, do not create an under-18 termination branch.
- When conditions cover a range, inspect the first, middle, and last question and then enumerate every target. Do not assume a range applied to all items. A condition marker on Q9 and Q13 is not evidence that Q10–Q12 also have it.
- For a typical pre-survey: online Q4–Q8 route to channel answers A/C; store Q9–Q13 route to B/C; comparison-only questions route to C; general Q14 onward routes to all valid purchasers. Adapt the numbers when the actual inventory differs.
- Optional open feedback and contact questions must not be made required by a global “make all required” action. Required status must be checked question by question.
- For questions such as “最多选择3项”, verify the editor's limit and the preview's visible limit. The option text alone is not enough.
- Matrix items in one block must use the same scale and direction. Avoid mixing agreement scales with willingness scales without a clear instruction.
- Do not use a compound question to measure two outcomes. Split “increase purchase frequency or spending” when the results need separate interpretation.
- For age grouping, make “未满18岁” a normal group unless the user explicitly requests termination. Do not silently turn it into a screening failure.

## Self-validation protocol

Run this protocol before reporting that the questionnaire is ready. If any check fails, fix it and run the failed check again in the same turn.

### A. Structure

Confirm the title, introduction, total question count, numbering, question types, option labels, matrix scales, and open-text settings. Confirm no duplicate or missing item was introduced by import.

### B. Routing matrix

Create a small matrix with these paths and expected visible blocks:

1. non-purchaser: termination only;
2. online-only: online block, not store/comparison;
3. store-only: store block, not online/comparison;
4. both: online + store + comparison/integration.

For each path, verify the first question after the branch and the last question before the common ending. Check that optional feedback/contact questions remain reachable.

### C. Per-question condition audit

Enumerate all questions that should have conditions. For each, record the exact source question, allowed answer values, and whether the condition is present. Flag both missing conditions and accidental extra conditions. Do not accept a visual preview that merely happens to list all questions.

### D. Answer-state audit

Check required state individually. Required: screening, channel, factual basics, matrix ratings, and other questions needed for analysis. Optional: open suggestions, questionnaire criticism, and interview contact unless the user says otherwise. Check every stated “最多选N项” cap.

### E. Platform test

Use the platform's preview/test mode to simulate all four paths where supported. If a full simulation is unavailable, inspect editor conditions and clearly mark the untested portion. Reopen or refresh the editor after saving and verify the saved draft, not just unsaved controls.

### F. Final status

Report only what was verified: saved draft, preview status, routing paths checked, and publication status. If publication was not explicitly requested, say it remains unpublished.

## WJX/问卷星 execution notes

When controlling 问卷星, use the current browser state and inspect the rendered controls or accessibility tree after each operation. Prefer exact question labels and visible condition markers. After editing a condition, refresh/reopen the design view before auditing it. If a confirmation dialog asks to clear or overwrite text, describe the consequence and proceed only when the user's instruction authorizes it.

When the request says “保存”, save the draft and verify the saved state. When it says “预览”, preview without publishing. When it says “发布”, perform the preflight and self-validation first, then publish only if the user has explicitly authorized publication in the current request.

## Delivery format

Give a concise result with:

- what was changed;
- the four-path routing result;
- required/optional and multi-select-limit checks;
- whether the draft was saved, previewed, or published;
- any unresolved limitation.

Do not claim “一次通过” unless the self-validation protocol completed successfully. If the platform still has a defect, name the exact question and branch and continue fixing rather than handing off a vague warning.
