# Ring builder front-end revamp: prompt for Freddie, draft v1

- From: Peter, 2026-11-13. For: Freddie, the front-end developer (`nore-freddie`).
- Status: REPLACED on 2026-11-13 by `freddie-clip-tour-builder-prompt.md`. The owner now wants
  the builder built around the guide clips, and the old front end has been deleted. Kept for the
  record. It was a DRAFT, untested, and never in the Prompt Library.
- How to use: the owner pastes the block under "The prompt" into Freddie's chat. Peter does not
  send it or install it.
- Source: the owner's request and ChatGPT's text (pasted 2026-11-13), the owner's two additions
  ("if its unclear let it ask me questions till it gets the flow properly"; "the additions should
  be almost like a zoom in to a part of the ring so its more clear for the customer"), and what
  Freddie's and Perry's records show (read only, 2026-11-13).

## What Peter changed, and why

| ChatGPT's text | In the prompt | Why |
|---|---|---|
| "You are the lead UX designer and frontend engineer" | Addressed to Freddie as a project; his own rules stay | Freddie already has a role and standards. A second role would compete with them. |
| "audit, plan, implement" in one run | Three stages; no building until the owner says the flow is right | The owner's addition: ask until the flow is right. |
| No zoom-in | A full section on showing additions as a zoom-in on the part | The owner's addition. |
| "Do not build an expensive 3D system unless..." | No 3D in this project | The owner cancelled the 3D plan on 2026-11-13 (Perry's log, RB-1 L-14). No 3D models exist. |
| "pricing", "checkout", "analytics", "saved configurations" | "Keep the integrations that really exist"; no price | The builder shows no price and ends in an enquiry. Peter never invents a price. |
| "I'm not sure, help me choose" and "needs jeweller review" as requirements | Two ideas Freddie proposes; the owner decides | Both change what is submitted (Becky's side) and how the business answers a customer. |
| "Create a central source of truth for compatibility" | Anything touching the catalogue, server validation or submitted data goes to Becky first | Those are shared with Becky under Freddie's own rules. |
| Long lists on mobile, accessibility and code hygiene | Shortened to the points specific to this project | Freddie's CLAUDE.md already holds those standards in full. |
| Nothing on money | New paid image runs need a named amount | Freddie's records show a spend hold until 1 December. |
| Nothing on the moving catalogue | Record the commit the audit is based on | The catalogue changed several times on 11 to 12 November. |

Peter's reading, to be confirmed by the owner: "the additions" means the add-ons and extras a
customer can add to a ring. The prompt tells Freddie to confirm this in his first question.

## The prompt

```text
Freddie, this is a project from the owner: revamp the ring builder's front end so that a customer with no jewellery knowledge can build a ring without getting lost. Read all of it, then reply as described under STAGE 1. Change no code in that reply.

Your CLAUDE.md, your RULES and your security rules all still apply. Nothing here loosens them. Where this is stricter, this wins.

THE PROBLEM
Customers find the builder confusing:
- too many choices appear together;
- it is unclear how the choices relate to each other;
- they cannot tell where a detail goes on the ring.
The code behind it has also become messy and needs inspection and clean-up.

THE GOAL
A simpler builder that feels like a guided consultation with a kind, knowledgeable jeweller: one clear decision at a time, and for every detail the customer can see where on the ring it goes.

WHAT THIS PROJECT IS NOT
- Not a 3D project. I cancelled the 3D plan for now. No 3D engine, no new framework, no build step. A clear, honest, picture-based experience is what I want. If you believe a new library is truly needed, that is a written proposal for my decision, as your rules already say.
- Not a catalogue change. You do not add, remove, rename or price options, and you do not change which combinations are allowed. If the audit shows the catalogue itself confuses customers, tell me. I decide.
- Not a back-end change. The catalogue data, the server's validation and what gets submitted are shared with Becky. Anything that touches them goes to her as a handoff first.

THE TWO THINGS I CARE ABOUT MOST

1. Ask until the flow is right
If anything about the flow is unclear, ask me. Keep asking, round after round, until you could draw the whole journey without guessing.
- Each round: show me the flow as you understand it now (a step list or a simple picture), then at most five questions, most important first.
- Each question comes with your recommended answer and what it would change.
- Say which answers you need before building and which can wait.
- Never fill a gap with your own guess about how I sell rings.
- Do not start building until I tell you the flow is right.

2. Additions are shown as a zoom-in on the ring
My words: "the additions should be almost like a zoom in to a part of the ring so its more clear for the customer".
"Additions" is read here as the add-ons and extras a customer can add to a ring (for example the Halo and Cathedral extras, stones on the bridge, two-tone claws, accent stones and birthstones, engraving). Your catalogue wins over this list. Confirm this reading with me in your first question.
- When the customer reaches an addition, the view starts on the whole ring and moves in to the part where the addition goes. Then it shows the addition there.
- The angle fits the part. A detail under the stone needs a side or underside view.
- A small whole-ring marker shows which part they are looking at. One tap returns to the whole ring.
- One short, plain sentence says what the part is. Use my corrected part names (the gallery rail and the bridge are different parts): C:\Users\OCIGU\Documents\nore-prompter\drafts\jewellery-glossary.md (read only).
- Pictures are honest. A picture must truly show the option it is labelled with. If a close-up is not the customer's exact ring, label it "Illustration". Never present it as a photo of their finished ring. The "Concept render" label rule is unchanged.
- With reduced motion switched on there is no movement: show the close-up and the marker directly.
- Reuse pictures I have already approved first. List every close-up that is missing. A new paid image run needs my approval for a named amount. Your records show a spend hold until 1 December.
Tell me whether the main steps (stone, setting, band) should use the same zoom-in. Recommend. I decide.

REQUIREMENTS FOR THE JOURNEY
- Show the decision that matters now. Reveal further details only when they apply.
- A starting order to test, not a decision: overall ring style; centre stone; setting and how the stone is held; band and metal; optional personal details; review and enquiry. Change it to fit the real dependencies and today's builder. Not too many steps, and no essential choice buried.
- Every step has one purpose and asks one plain-language question.
- Options are picture cards with an obvious selected state. Any jewellery term gets one short sentence of explanation.
- Overall ring styles, how the stone is held, and decorative details are never mixed in one list. Check every term that could mean two things, and say which part of the ring it describes.
- Required choices are clearly separate from optional ones. Optional refinements sit behind one clear control (for example "Personalise further").
- Nothing optional is pre-selected. A default is never shown as the customer's decision.
- Progress is visible. Back and Continue are always available. A summary is always within reach, and any earlier choice can be edited from it without starting again. Choices are kept when moving between steps.
- One obvious main action per screen.
- Choices that do not fit are not offered. Where a missing choice would puzzle a customer, one short line says why.
- Before a change to an earlier choice removes later ones, say which will be affected. Never replace a choice silently. A cleared choice is cleared in the submitted data too.
- Review shows every chosen feature, the optional details left out, and anything undecided, with an edit link per section. The destination stays what it is today.
- Natural or lab-grown stays stated exactly, for every stone.
- Phone first: most customers arrive on a phone. Sticky controls never cover options, error messages or the keyboard. No sideways scrolling, no tiny swatches, no long unexplained dropdowns. Your own standards for accessibility, speed and brand apply in full.
- Every option a customer can pick today stays reachable. Simplify how they find it. Anything you would remove is a question for me, never a silent deletion.

TWO IDEAS TO PROPOSE, NOT BUILD
Both change what is submitted and how we answer a customer, so they need my decision and Becky's contract.
- "I'm not sure, help me choose" on the steps where it makes sense, carried through to the enquiry.
- "Needs jeweller review" for a combination that needs assessment, where today it is simply not offered.
Tell me where each would help and what it would change. Build neither until I say yes.

NEVER INVENT
A price or estimate (the builder shows none today), a manufacturing rule or guarantee, a delivery promise, a supported option, or a compatibility rule. Mark each restriction CONFIRMED (a file or my words) or ASSUMED, and bring the unresolved ones to me.

STAGE 1: AUDIT AND PROPOSED FLOW (your first reply; no code changes)
Start from what exists (your own revamp plan and audits, Becky's flow audit). Say what you reused, and re-check it against the latest main. The catalogue has been changing daily, so name the commit your audit is based on.
A. What you inspected, on which screen widths and paths, and what you could not inspect or test. Claim nothing you did not check.
B. The audit: customer problems, most serious first. Each one VERIFIED (say how) or ASSUMED. Include confusing terms, overlapping choices, duplicate controls, misleading pictures, dead ends, invalid combinations, and choices that vanish or reset.
C. The option map: every option that exists today. For each: its id, the customer label, what it is in one sentence, where on the ring it goes, the step it is in today, what it depends on, what it conflicts with, what is submitted, and whether its picture truly shows it.
D. The proposed journey: each step, the question it asks, required or optional, and where every option from the map now lives.
E. The zoom-in plan: for each addition, the part, the view angle, the picture you have today or MISSING, and exact or illustration. Then two ways to build the zoom-in with the effort and cost of each, and your recommendation.
F. Your questions for me.

STAGE 2: BUILD (only after I tell you the flow is right)
- First show me a build plan: small milestones, each with pass/fail checks, the files it touches and anything it needs from Becky. The first milestone is one complete path through the new flow, including one zoom-in addition, from the first step to a submitted test enquiry.
- Then carry on in a development branch without asking me for each milestone. Stop and ask only for: a business decision, a new dependency, a change to the catalogue or to what is submitted, or a paid run.
- Clean up as you go, in small steps and without a broad rewrite: option definitions, compatibility rules, design state, screens, picture mapping and submission kept apart; one design state that the screens, the summary and the submission all read; stable option ids, never labels. Remove unused code only after checking what refers to it. Keep every integration that really exists.
- Handle loading, a missing picture, a validation error and a failed submission clearly.
- After each milestone report: what changed, what was tested, each check PASS, FAIL or NOT RUN, and what is unresolved. Give me a preview I can open on my phone, and tell me how.

STAGE 3: VERIFY
Build the test list from the real dependencies. Cover at least:
- a simple ring with nothing optional, and a heavily customised one;
- every top-level style and each major branch;
- changing an early choice after finishing later steps;
- invalid combinations and stale hidden values;
- skipped optional details;
- Back, and editing from the review screen;
- a refresh, if saved state is supported;
- a missing picture;
- a failed submission and a retry;
- phone layouts, keyboard use and reduced motion;
- every addition's zoom-in showing the right part.
The submitted data must match the visible summary exactly. Use test enquiries only, marked the way you mark them today. Send nothing to a real customer. Do not call the builder ready on a successful build or on screenshots alone. Going live needs my approval for that merge, with the reviews your rules require.

DONE WHEN
- A customer can tell what each decision changes and where it sits on the ring.
- Only the choices that apply appear, at the right time.
- Every option that existed before can still be reached.
- No choice is silently lost, replaced or wrongly submitted.
- Phone and desktop both work from the first step to the enquiry.
- The integrations that exist still work.
- The option and compatibility rules are documented, and the code is easier to maintain.
- I have a working preview, a short before-and-after explanation, the test evidence and the list of what is still limited.

MOST LIKELY WAYS TO GET THIS WRONG
- Building before the flow is agreed, because the audit made the answer look obvious.
- A zoom-in that looks good but shows a different ring from the one the customer chose, with no "Illustration" label.
- Simplifying by quietly dropping options.
- Tidying code that Becky's server depends on without a handoff.
- Asking one question at a time, or asking in the abstract with no flow to react to.
```
