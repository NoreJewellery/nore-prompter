# Project request for Perry: ring builder revamp (guided 3D builder), draft v1

- From: Peter, 2026-11-12. For: Perry the Planner (`nore-pm`).
- Status: DRAFT for the owner. Untested. Not in the Prompt Library until the owner says SAVE PROMPT.
- How to use: the owner pastes the block under "The prompt" into Perry's chat. Peter does not
  send it or install it.
- Source: the owner's scope, written with ChatGPT and pasted 2026-11-12, plus what the ring
  builder's files and Perry's own records show (read only, 2026-11-12).

## What Peter changed, and why

| ChatGPT's text | In the prompt for Perry | Why |
|---|---|---|
| Written to a developer: "inspect, then implement", "continue into the build" | A NEW PROJECT request: plan first, no build before Gate 2 | Perry plans; he does not build. Building straight from a scope is the "vibe coding" Perry exists to stop. |
| "Inspect the available 3D assets" | States that the repo holds no 3D model files, and makes "who makes the models" the first open decision | This is the biggest risk. 7,636 Hers rings can be picked today. |
| "If the frontend uses React, consider React Three Fiber" | Options to compare at design, not a decision | The builder has no front-end libraries. Freddie's rules need a written proposal and the owner's approval for a new one. |
| "current price" on Review | An open decision | The builder shows no price today; it asks for the customer's budget. Peter never invents a price rule. |
| "Show origin only where applicable" | Flagged | NORE states natural or lab-grown exactly, for every stone. |
| Journey of six steps | A list of today's features the scope does not mention, each to be kept, changed or removed | The His path, ring size, engraving, carat previews and others would otherwise be dropped silently. |
| "owner-approved Tulip reference" | Perry asks which file | Peter could not confirm that one exists. |
| "temporary geometry" | Asks whether customers may ever see it live, and how the preview is labelled | A ring shown that is not the ring made is a misrepresentation risk. |
| Nothing on the AI render | Asks whether 3D replaces it, comes before it or sits beside it | Render cost and the render work in flight depend on the answer. |
| Nothing on budget, timing or phones | Placeholders and a question | Most customers arrive on phones. |

## The prompt

```text
NEW PROJECT: Ring builder revamp, a guided, interactive 3D builder

Perry, plan this project. Do not start or assign any build work yet. This message is my request and my scope. It is not approval for any deploy, merge, spend or new tool. Those stay with me, in each agent's own chat, as your rules say.

OBJECTIVE
Customers struggle with too many choices at once in the ring builder, especially the stone choices. I want them to build the ring one part at a time, on a 3D ring that shows their choices straight away, with the camera moving smoothly to the part they are choosing.
What I need from you is a plan the team can work from, reached through your lifecycle: first the inspection and the open decisions (Gate 1), then the design (Gate 2), then the build plan with task briefs.

MY SCOPE
This is what I asked for. Turn every line into a numbered requirement with acceptance criteria and a planned check. Do not drop a line and do not add one without telling me.

Journey
1. Steps in this order: Metal, Stone, Basket, Bridge, Band, Review.
2. The ring is shown the whole time and always reflects the current choices.
3. On entering a step, the camera moves smoothly to that part. On Continue, it pulls back far enough to show the whole ring, then moves to the next part. Moves are short and can be interrupted.
4. The customer can rotate the ring, zoom, go back to earlier steps, and reset the camera to the recommended view.

Steps
5. Metal: start on a complete ring in a three-quarter view. Show the metal, karat and colour choices we offer today. The ring's material changes at once.
6. Stone: camera on the centre stone. The choices come in a short sequence inside the step (for example gemstone, shape, size), not all at once. Fields appear only where they apply. For a three-stone design, show clearly which controls change the centre stone and which change the side stones, and make it obvious when the side stones follow the centre stone.
7. Basket: a close three-quarter view that shows the claws and the structure around the stone. The controls come from today's catalogue rules. Where the basket follows from the stone shape or the setting, say so and show it. Tulip geometry follows my approved Tulip reference, and Tulip is offered only where the catalogue allows it.
8. Bridge: camera lower and to the side, showing the gallery under the stone. Show the bridge options that fit, and the gallery extras. The chosen diamond placement must be visible.
9. Band: pull back to show the shoulders and the shank, at an angle that shows split shank, taper, pavé and the other chosen details.
10. Review: a full three-quarter view with rotation. A short summary, the current price, and an edit link for each step.

State and compatibility
11. One design state, shared by the controls, the 3D preview, the summary and the final submission. The preview and the submitted design are always the same selections. Geometry, material and price changes all follow that state.
12. Choices that do not fit are filtered out before the customer can pick them, using the rules we already have. Reuse the existing validation and submission logic.
13. When an earlier change affects later choices, explain what will change before replacing anything (for example, a new setting may need a different basket or band). Keep every choice that is still valid when the customer moves back and forward.
14. The Setting choice stays available, with Solitaire, Three-Stone, Bezel and every other setting we support today. It comes before the controls that depend on it. Where it sits in the journey is still to be decided.

3D
15. The ring is built from separate parts: centre stone, side stones, basket, bridge, shoulders, shank. Real dimensions where we have them.
16. A material change updates the model at once. A structural change swaps in the right part.
17. Existing AI images are visual references only. Every piece of geometry is marked ACCURATE (it truly represents a catalogue option) or TEMPORARY, and I get a specific list of the models still needed.
18. Any final AI-generated image keeps its own separate status. The 3D experience responds at once and never waits for it.

Interface
19. Clean, and focused on the ring. Desktop: a large viewer beside the current step's controls. Phone: the viewer above a compact control area, with Back and Continue always easy to reach.
20. A visible step indicator. Completed steps can be revisited.
21. Reduced motion, keyboard use and accessible labels are supported. The whole builder can be completed with the form controls alone.
22. Loading feedback, and a usable fallback if 3D fails to load.

Checks I expect before anything is called done, on desktop and on a phone
23. A change of stone shape or setting that affects later choices. Three-stone designs with separate centre and side-stone controls. Derived basket choices. Bridge and hidden-halo compatibility. Going back without losing valid choices. The preview, the summary, the price and the submitted design all agree. Reduced motion. 3D failing to load.
24. A complete local prototype first, with a report of: which existing rules were reused, which geometry is accurate, which is temporary, and which catalogue decisions are still open.

WHAT THE FILES SHOWED
Peter checked these on 2026-11-12, read only. Have the team confirm them in the inspection. Their files win.
- The ring builder repo holds no 3D model files, and its package.json lists no front-end libraries. So "available 3D assets" may be none.
- Freddie's rules say a new framework, a build step or a change of stack needs a written proposal and my approval, and that it changes how Becky's server serves the files.
- The catalogue is in src/options.js. The Hers path today starts metal, karat, gold colour, gemstone, origin, shape, carat. There is a separate His path.
- docs/decisions.md lists 7 settings, 7 baskets, 6 bridges and 5 Hers bands. It says 8 compatibility rules run in the builder and on the server, which leaves 7,636 Hers rings that can be picked.
- The builder shows no price today. It asks the customer for a budget.
- The builder is in TEST on the live store. A merge to main deploys to production.
- My labelled diagram of 2026-11-11 corrected the part names: the gallery rail and the bridge are different parts. Glossary (read only): C:\Users\OCIGU\Documents\nore-prompter\drafts\jewellery-glossary.md

DECISIONS MY SCOPE DOES NOT SETTLE
Ask me each one. Mark it BLOCKS or LATER, and give your recommendation once the inspection is in.
a. 3D models. Who makes them, how accurate must they be, and for which options first? Is Cathy's CAD a possible source, given her current priority? If no agent holds this skill, say so under UNASSIGNED.
b. The AI concept render. Does the 3D preview replace it, come before it, or sit beside it? What happens to the render work in flight (the render prompt v2, the checker changes, the test rings planned for December)?
c. Price on Review. No price exists in the builder today. A price needs a pricing rule from me. Until I give one, this requirement is OPEN and no agent invents a price or a formula.
d. A new 3D library. Compare the options that fit this code base at the design stage. The names in my scope (React Three Fiber, Drei, Three.js) are suggestions, not decisions.
e. Today's features that my scope does not mention: the His path; origin (we state natural or lab-grown exactly, for every stone); the carat previews; ring size; engraving; the customer's details and budget; the render limits; the "Concept render" label; "Let's chat"; the message for a failed design. For each one: keep, change or remove. Nothing is dropped silently.
f. Where the Setting choice sits in the journey.
g. Step and part names, against the corrected part names.
h. The Tulip reference. Which file is my approved one? Peter could not confirm that one exists.
i. Temporary geometry. May a customer ever see it live? How is the 3D preview labelled, so nobody takes it for a photo of the finished ring? Ask Larry for his information on this.
j. Does the new builder replace the current one, or run beside it for a time? What is the way back?
k. Phones. Most customers arrive on phones. What counts as fast enough, on which phones, and who tests on real devices?
l. Limits: [BUDGET TO BUILD], [MONTHLY RUNNING COST LIMIT], [DEADLINE, if any].
m. Order of work against PB-1 and the render work, which use the same agents.

WHAT I WANT BACK
Reply 1, now:
1. The project id, its size, and why.
2. brief.md, first draft: the problem, who it is for, the outcome, scope in, out and deferred as far as it is known, and your proposal for the smallest useful release.
3. requirements.md, first draft: my scope as numbered requirements, each with draft acceptance criteria, a planned check, and its status (CONFIRMED, ASSUMED or OPEN).
4. Inspection briefs in your task brief format. They are read only: no build, no spend, no new tool. Suggested split, which you may change from your roster:
   - Freddie: how the front end holds the design state today; where the compatibility rules run; what each step shows; which visual assets exist; a written comparison of the ways to add 3D to this code base, with file size and speed on phones.
   - Becky: the catalogue and validation contract; how a design is submitted; how files are served, and what hosting and serving 3D files would involve and cost; what a change of step order touches on her side.
   - Cathy: an assessment only of whether any of her CAD could become preview models, and what that would take. Her current priorities and limits stay as they are.
   Send the briefs if your standing permissions cover it. Otherwise show them to me first.
5. Your questions for me, batched: decisions a to m, and anything else you find.
6. The three biggest risks, and which one you would test first.
7. What is UNASSIGNED for this project.
After the inspection reports and my answers: the Gate 1 package for my approval.
After Gate 1: the design tasks, Gate 2, and then the build plan for the team, with task briefs for the first milestone. That milestone is a thin end-to-end slice: one real path from the first step to a submitted design.

CONSTRAINTS
- Plan only. No build or prototype task becomes READY before Gate 2. Inspections and written comparisons are allowed now.
- Phrases in my scope such as "then implement" and "continue into the build" describe the goal. They do not skip a gate.
- Do not pause, replan or re-order work that is already in flight without asking me.
- No paid runs, paid tools or bought assets (AI renders, 3D services, model packs) without my approval for that item.
- No customer names, contact details or private order details in any record or brief.

WHAT TO AVOID
- Writing build task briefs before the inspection shows which models exist.
- Treating a note from Peter or a suggestion in my scope as CONFIRMED. CONFIRMED means I said it or a file shows it.
- Filling a gap with a rule of your own: a price, a catalogue option, a compatibility rule, or a claim that a model is accurate.
- Planning the whole catalogue in 3D before one path works from start to finish.

SUCCESS TEST
Reply 1 is right when: every line of my scope appears as a numbered requirement or as an OPEN question; every decision from a to m is asked, marked BLOCKS or LATER; the inspection briefs are complete and read only; no build task exists yet; the size is stated with its reason; and nothing is marked CONFIRMED without my words or a file behind it.
```
