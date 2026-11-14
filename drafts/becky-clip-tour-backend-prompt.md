# Back end for the new clip-based ring builder: prompt for Becky, draft v1

- From: Peter, 2026-11-13. For: Becky, the back-end developer (`nore-backend`).
- Status: DRAFT for the owner. Untested. Not in the Prompt Library until the owner says SAVE PROMPT.
- How to use: the owner pastes the block under "The prompt" into Becky's chat. Peter does not
  send it or install it.
- Goes with: `freddie-clip-tour-builder-prompt.md` (commit b32e218), Freddie's brief for the
  front end.
- Source: the owner's request of 2026-11-13 ("we also need the backend to match what freddy
  builds"), the owner's eight answers recorded in Freddie's brief, and Becky's own files (read
  only, her ring-builder copy at commit 34d1cae).

## What Peter found, and what it led to in the prompt

| Found in Becky's files | In the prompt |
|---|---|
| Builder files are served by the Lambda through the Shopify app proxy (`/proxy/assets/*`). No CDN in template.yaml. | Video hosting is the first thing to settle: file size, byte-range requests on phones, caching, cost. Options compared, not assumed. |
| The stills and clips are only in `ring-guide-output/`, which is gitignored. | Back them up first. They are the owner-approved originals and exist in one place. |
| `/options.json` already sends the steps, the paths and the compatibility rules. | Keep the server as the one source of truth; the new front end reads the rules from it. |
| The Hers path is a fixed list ending `..., extras, ringSize, engraving, notes`. | Ring size and engraving move to the first screen; the order of parts is not approved yet, so nothing is hard-wired to an order. |
| Ring sizes are a list of numbers. | "Unknown" is a new value: every place that expects a number is listed. |
| His path and the Fiorella signature setting exist. | Nothing is deleted. What the server does with them in the first release waits for the owner's answer. |
| No staging site exists in the records. | A plan for a preview the owner can open on a phone while the live builder stays paused. |

## The prompt

```text
Becky, this is a project from the owner: make the back end match the new ring builder front end that Freddie is building. Read all of it, then reply as described under STAGE 1. No code change, no deploy and no spend in that reply.

Your CLAUDE.md, your RULES and your security rules all still apply. Nothing here loosens them. Where this is stricter, this wins.

WHAT IS BEING BUILT
The old builder front end is deleted and the builder is paused. Freddie is building a new one around the ring guide clips you made. His brief is at C:\Users\OCIGU\Documents\nore-prompter\drafts\freddie-clip-tour-builder-prompt.md (read only). What I have decided:
1. First screen, before the tour: the metal, the ring size and the engraving. Ring size has an option for "unknown".
2. Then the interactive ring: a guided tour of the parts, with a strip of part names for jumping to any part. At each part the clip plays and that part's choices appear.
3. The order starts top to bottom: centre stone, prongs, head, shoulders, bridge, shank, base. Freddie may propose a different order where the rules need it. It is not final until I approve it.
4. The clip is a guide, labelled "Illustration". It never changes with the customer's choices.
5. The ending is the same as before: review, the customer's details, the AI concept render with its "Concept render" label, then "Let's chat".
6. Women's engagement rings first. His rings and Fiorella come later.
Freddie will not build until I tell him the flow is right. His first reply includes a list of what he needs from you.

YOUR PART

1. The guide pictures and clips
- First, back up the approved originals (2 stills, 7 clips with their 1080, 720 and poster files). Your notes say they are in a folder that is not committed, so they exist in one place.
- Then work out how they reach a customer's phone. Check and report, do not assume:
  - whether today's route (the Lambda behind the Shopify app proxy) can serve files of this size at all;
  - whether it answers byte-range requests, which phone browsers may need to play video;
  - caching, and what a full tour costs to serve.
- Compare at least two ways to host them, each with its cost per month, the effort, the risk and the way back. Recommend one. A new service or a new recurring cost needs my approval, as your rules say.

2. The catalogue contract
- The server stays the one source of truth for options and compatibility rules. The new front end reads them from the server and keeps no copy of its own.
- Ring size and engraving move to the first screen with the metal. If any rule today makes one of them depend on a later choice, tell me.
- The grouping of options into parts, and the order of parts, come from Freddie's option map once I approve it. Until then, tie nothing to an order.
- Option ids stay stable. Renders, the dashboard and saved enquiries depend on them. No option is added, removed, renamed or re-ruled by this project.
- Write the contract down, with a version, before Freddie builds against it.

3. Ring size "unknown"
List every place that expects a number today: the server's checks, storage, the dashboard, the emails, the CAD sheet, the render. Say what each must do with "unknown". Earlier enquiries must still read correctly.

4. Submission
- The server stays the final judge. A combination that does not fit is refused, and a value left over from an earlier choice never gets through.
- A refusal says which choice is wrong, in a form Freddie can turn into a clear message. Put this in the contract.
- Check what happens today when a submission fails and the customer tries again. It must not create two enquiries.
- What is stored must match the summary the customer saw.

5. The ending
The AI concept render, its checks, its caps and limits, the emails and "Let's chat" keep working with answers that now arrive in a new order and with an unknown ring size. The render prompts are not yours to change.

6. His rings and Fiorella
Delete nothing. Freddie is asking me what those visitors see in the first release. Follow that answer for what the server offers and accepts.

7. Preview, pause and go-live
- I need to open Freddie's work on my own phone while the live builder stays paused. Your records show no staging site. Give me the options, with cost and risk.
- Unpausing is a production change. It needs my approval for that deploy and the reviews your rules require. Say what the way back is.

NOT YOURS IN THIS PROJECT
The front-end code, the render prompts, new features nobody asked for (analytics, prices), and any change to what we sell.

NEVER INVENT
A price, a visitor count, a cost, a rule or a test result. Use what your tools show, cite it, or mark it UNVERIFIED.

WORKING WITH FREDDIE
- The contract comes first. He builds against it, and it never changes silently.
- If his list of needs has not arrived yet, do the work that does not depend on it: the back-up, the hosting comparison, the "unknown" list, the inventory, the preview options.
- Where his design and the server's rules disagree, say so to him and to me. Do not quietly bend either.

QUESTIONS FOR ME
Ask in rounds of at most five, most important first, each with your recommended answer and what it changes. Say which answers you need before building.

STAGE 1: YOUR FIRST REPLY (no code change, no deploy, no spend)
A. What you read and checked, with the commit, and what you could not check.
B. The inventory: every piece of the server the builder depends on (routes, catalogue, rules, submission, render, emails, dashboard, pause). Mark each NO CHANGE, MUST CHANGE, or WAITS FOR THE APPROVED FLOW.
C. The guide files: where the originals are backed up, or your plan for it; the hosting options compared; your recommendation and its cost.
D. The contract, as a DRAFT: the catalogue, the submission and the refusals. Mark what waits for the approved order.
E. The "unknown" ring size list.
F. The preview options.
G. The three biggest risks, and which you would test first.
H. Every approval you will need from me, one line each: what, what could go wrong, how to undo it.
I. Your questions for me.

STAGE 2: BUILD (after I have told Freddie the flow is right, and you have his list)
On a branch, in small commits, with tests for everything that touches customer data or the submission. The contract gets its version. Nothing deploys.

STAGE 3: VERIFY AND DEPLOY
- Mark every check PASS, FAIL or NOT RUN, with the output.
- Test with Freddie's branch from the first screen to a stored enquiry: a simple ring, a heavily customised one, ring size "unknown", an incompatible combination sent straight to the server, a failed submission and a retry.
- The clips play on a real phone, including an iPhone. That check is mine; tell me exactly what to open.
- Test enquiries only, marked as you mark them today. Nothing goes to a real customer.
- Rehearse the pause and the way back before the real unpause.
- Deploy only with my approval for that merge. Log it in ACTIONS.md.

DONE WHEN
- The clips and stills load and play on phones, from a home that is backed up, at a monthly cost I have approved.
- Freddie's front end gets its options and rules from one written, versioned contract.
- "Unknown" ring size works everywhere a ring size is used.
- Nothing that does not fit can be stored, and a retry never makes a second enquiry.
- The render, the emails, the dashboard and "Let's chat" still work.
- I can preview on my phone before go-live, and the way back is tested.

MOST LIKELY WAYS TO GET THIS WRONG
- Serving video through a route that cannot stream it, and finding out on a customer's phone.
- Building to the top-to-bottom order before I have approved the order.
- Letting the front end keep its own copy of the rules.
- Treating "unknown" as a front-end label while the server still expects a number.
- Unpausing to let me preview.
```
