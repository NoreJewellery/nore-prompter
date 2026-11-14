# New ring builder front end built around the guide clips: prompt for Freddie, draft v1

- From: Peter, 2026-11-13. For: Freddie, the front-end developer (`nore-freddie`).
- Status: DRAFT for the owner. Untested. Not in the Prompt Library until the owner says SAVE PROMPT.
- How to use: the owner pastes the block under "The prompt" into Freddie's chat. Peter does not
  send it or install it.
- Replaces: `freddie-ring-builder-frontend-revamp-prompt.md` (commit 9e4baec), which was written
  before the clips existed and before the old front end was deleted.
- Source: the owner's request of 2026-11-13 ("instead of steps have him implement the clips in a
  3d format along with the proper choices in each step"), the owner's eight answers below, and
  Becky's and Freddie's own records (read only, 2026-11-13).

## The owner's answers (2026-11-13)

| Question | Answer (owner's words where quoted) |
|---|---|
| How does a customer move through the builder? | "Guided tour plus tap a part" |
| The clips show one white gold radiant. What if the customer picks something else? | "Clip is a guide": labelled "Illustration"; the customer's own choices show on picture cards and in the summary |
| Clip 7 (base) shows the ring tipping over | "Use clip 7 as it is" |
| What happens after the last part? | "Same as before": review, the customer's details, the AI concept render, "Let's chat" |
| May Freddie change the top-to-bottom order if the rules need it? | "Freddie proposes, I approve" |
| Where is the metal chosen? | "before we even start have a screen to choose metal then go into the interactive ring builder" |
| Which rings at first? | "Hers first, the rest later" |
| Where are ring size and engraving chosen? | "first screen with the metal; have an option for unknown" |

Peter's readings, which Freddie is told to confirm: "3d format" means the clips give the 3D feel,
with no 3D engine; "an option for unknown" belongs to ring size.

## What the records showed (2026-11-13)

- Freddie's INBOX: the old builder front end was deleted on 2026-11-13 on the owner's instruction
  and the builder is paused. `src/page.js` still loads the deleted files.
- Becky's ACTIONS.md, rows 166 to 178: 2 stills and 7 clips were made for about $6.37. The owner
  kept all of them ("Keep all as is"). The files are in `nore-backend/ring-guide-output/` and are
  not committed. Becky's notes list three flaws: clip 1 starts with the top of the stone cut off
  and swings to a front view; clip 6 swings to a 3/4 view first; clip 7 does not reach the base.

## The prompt

```text
Freddie, this is a project from the owner: build the new front end of the ring builder around the ring guide clips. Read all of it, then reply as described under STAGE 1. Change no code in that reply.

Your CLAUDE.md, your RULES and your security rules all still apply. Nothing here loosens them. Where this is stricter, this wins. Where it differs from any earlier revamp brief, this one wins.

WHAT I WANT
My words: "instead of steps have him implement the clips in a 3d format along with the proper choices in each step".
The old builder showed one screen of choices after another. The new one keeps the ring on screen. The camera moves to one part of the ring, and the choices for that part appear with it. The customer always sees where on the ring their choice goes.
"3d format" is read here as: the clips give the 3D feel. There is no 3D engine, no new framework and no build step. If you read my words differently, ask me before anything else.

WHAT EXISTS (checked on 2026-11-13; your files and Becky's win over this list)
- The old builder front end is deleted and the builder is paused. Your INBOX says src/page.js still loads the deleted files.
- The guide ring: 2 stills and 7 clips, in C:\Users\OCIGU\Documents\nore-backend\ring-guide-output\ (Becky's folder, read only, not committed).
  - picture1.jpg: the whole ring, 3/4 view. picture2.jpg: the whole ring from the side.
  - Clips 1 to 7, each as clipN-1080.mp4, clipN-720.mp4 and clipN-poster.jpg: square, silent, about 8 seconds. 1 centre stone, 2 prongs, 3 head, 4 shoulders, 5 bridge, 6 shank, 7 base.
  - Clips 1, 2 and 4 start from the 3/4 picture. Clips 3, 5, 6 and 7 start from the side picture.
  - Becky's notes: clip 1 starts with the top of the stone cut off and swings to a front view; clip 6 swings to a 3/4 view first; clip 7 does not reach the base, the ring tips over. I kept all seven as they are.
- The catalogue, the server's checks, the AI concept render and the enquiry are Becky's side and are still there.

WHAT I HAVE DECIDED
1. First screen, before the tour: the customer chooses the metal, the ring size and the engraving. Ring size has an option for "unknown". ("Unknown" is read here as belonging to ring size, since engraving is already optional. Confirm with me.)
2. Then the interactive ring. A guided tour: Continue plays the clip to the next part and shows that part's choices; Back returns. A small strip of part names also lets the customer jump to any part.
3. The order starts top to bottom, as the clips run: centre stone, prongs, head, shoulders, bridge, shank, base. If the catalogue's rules need a different order, propose it and say why. Build only the order I approve.
4. The clip is a guide, not the customer's ring. It always carries the label "Illustration". The customer's own choices show on the picture cards and in the summary.
5. Clip 7 is used as it is.
6. The ending is the same as before: a review of every choice, the customer's details, the AI concept render of their own ring with its "Concept render" label, then "Let's chat".
7. Women's engagement rings first. His rings and Fiorella come later.

HOW THE TOUR MUST BEHAVE
- One part at a time. Only the choices that belong to that part and fit the earlier choices are shown. Each part asks one plain question, and any jewellery term gets one short sentence, using my corrected part names: C:\Users\OCIGU\Documents\nore-prompter\drafts\jewellery-glossary.md (read only).
- Every option a woman's ring can have in today's catalogue has a home: the first screen, one of the seven parts, or the review. Nothing is dropped silently. An option that fits no part is a question for me.
- Choices are never held up by video. If a clip is slow, fails or cannot play, the poster or still shows and the customer carries on. The whole builder can be completed with no video at all.
- Moving between parts is short and can be interrupted. The clips start from two different pictures and three of them have flaws, so say how each move will look, including a jump from the strip.
- With reduced motion switched on, no clip plays: show the still of the part.
- Phone first. Do not download seven clips at once: the poster first, the 720 file on phones, the next clip only when it is likely to be needed. Clips play muted and in place, never full screen. Tell me the measured weight of the first screen and of a full tour.
- Progress is visible, a summary is always within reach, and any earlier choice can be edited without starting again. Nothing optional is pre-selected.
- Before a change to an earlier choice removes later ones, say which. Never replace a choice silently. A cleared choice is cleared in what gets submitted.
- Natural or lab-grown stays stated exactly, for every stone.
- Honest pictures: a picture card must truly show the option it is labelled with. Reuse pictures I already approved (they are in git history) where they still match the catalogue. A new paid image run needs my approval for a named amount.

BECKY'S SIDE (a handoff first, never your own change)
- Getting the clips and stills from her folder onto the site: where they live, how they are served and cached.
- The "unknown" ring size: it changes what the server accepts and what is submitted.
- Anything else that touches the catalogue, the server's checks, the render or the enquiry.
- Unpausing the builder. That also needs my approval for that merge, and the reviews your rules require.

NEVER INVENT
A price or estimate, a manufacturing rule, a delivery promise, a supported option or a compatibility rule. Mark each restriction CONFIRMED (a file or my words) or ASSUMED, and bring the unresolved ones to me.

ASK UNTIL NOTHING IS MISSING
I want you to ask me questions so that I am not missing anything. Keep asking, round after round, until you could draw the whole journey without guessing. Each round: show me the flow as you understand it now, then at most five questions, most important first, each with your recommended answer and what it changes. Say which answers you need before building. Do not build until I tell you the flow is right.
Cover at least these, which I have not decided:
- Where the overall style or setting is chosen, since it affects several parts.
- What a visitor who wants a His ring or Fiorella sees in the first release.
- The exact words that tell a customer the clip is an illustration and their ring will follow their choices.
- Which picture cards exist, which are missing, and what the missing ones would cost.
- Anything from the old builder that this design has no place for.

STAGE 1: YOUR FIRST REPLY (no code changes)
A. What you read and checked, with the commit, and what you could not check. Claim nothing you did not check.
B. The option map: every option of a woman's ring in today's catalogue, with its id, its label, where on the ring it goes, the part or screen it will live in, what it depends on, and whether an approved picture exists.
C. The proposed order of parts, with any change from top to bottom and the rule that forces it.
D. The screens as simple pictures, for a phone and for a desktop: the first screen, one part of the tour, the review.
E. How each move between parts will look, clip by clip.
F. What you need from Becky, as a list.
G. Your questions for me.

STAGE 2: BUILD (only after I tell you the flow is right)
- First show me a build plan: small milestones, each with pass/fail checks. The first milestone is one complete path: the first screen, two parts of the tour, the review, and a submitted test enquiry.
- Then carry on in a development branch without asking me for each milestone. Stop and ask only for: a business decision, a new dependency, a change on Becky's side, or a paid run.
- After each milestone report: what changed, what was tested, each check PASS, FAIL or NOT RUN, and what is unresolved. Give me a preview I can open on my phone, and tell me how.

STAGE 3: VERIFY
Cover at least:
- a simple ring and a heavily customised one;
- every setting and each major branch;
- ring size "unknown";
- changing an early choice after later ones;
- jumping from the strip, forwards and backwards;
- Back, and editing from the review;
- a clip that fails to load, and no video at all;
- reduced motion;
- a slow phone connection;
- keyboard use;
- a failed submission and a retry.
What is submitted must match the visible summary exactly. Use test enquiries only, marked the way you mark them today. Send nothing to a real customer. Do not call the builder ready on a successful build or on screenshots alone.

DONE WHEN
- A customer can see where on the ring each choice goes.
- Only the choices that apply appear, one part at a time.
- Every option of a woman's ring in the catalogue can be reached.
- No choice is silently lost, replaced or wrongly submitted.
- The builder works from the first screen to the enquiry on a phone and on a desktop, with video and without it.
- The clip is always labelled "Illustration", and the AI render "Concept render".
- I have a working preview, the test evidence, and the list of what is still limited.

MOST LIKELY WAYS TO GET THIS WRONG
- Building before the flow is agreed.
- Letting the clip stand in for the customer's ring, so a yellow gold oval is shown as a white gold radiant with no label.
- A builder that stalls when a clip is slow on a phone.
- Forcing an option into a part where it does not belong, to make the map look complete.
- Changing something on Becky's side without a handoff.
```
