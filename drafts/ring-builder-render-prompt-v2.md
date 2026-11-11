# Ring builder render prompt v2 (Hers): guide picture + short edit

- From: Peter (nore-prompter), 2026-11-11. For: the owner, then Freddie (nore-freddie).
- Status: **DRAFT. No render made with it yet.** Nothing here is live. Freddie applies it only
  with the owner's approval; every test render needs the owner's approval of that spend.
  The checker rules in Part 7 were replayed once on 35 judged pictures (run 41, Part 7a). The
  render prompts in Part 4 are still untested.
- Scope (owner, Nov 11): all of Hers (Solitaire, Three-Stone, Bezel, East-West). Fiorella keeps
  its own prompt. His is not covered.
- Owner's request: "im spending way too much on renders as so many fail; i need a new prompt
  based on my ring builder that will allow gemini to get the renders right the first time ...
  allow for re-renders if the view messes up".
- Odds, said before any spend: this method is proven on Fiorella only (8 approved pictures). On
  the normal rings it is a test, not a likely pass, until the test in Part 8 has run.

## 1. What is going wrong today (from Freddie's code and run notes, read only)

1. **The checker fails good pictures.** Run 30: 8 rings failed, and 6 of the 8 looked right by
   eye. Every false fail buys a re-render. The check prompt also says "if a detail ... cannot be
   made out, answer false", so anything the camera hides can fail a view.
2. **The prompt is 900 to 1,350 words per view and says each fact 3 to 5 times** in different
   words (band: 5 lines; prongs: 4; stone position: 4). Freddie's own Fiorella test (LESSONS F19)
   showed a long description makes Gemini redraw a ring, and a short edit of an approved picture
   holds it.
3. **The prompt contradicts itself.** Found by printing today's prompts for four sample rings:
   - Every top view says "with the shoulders sweeping up into the head". A Solitaire without
     Cathedral arches also says "no shoulders sweeping up".
   - "Stones on the bridge" ends "the shoulders and the band have no stones". On a Pavé band the
     band line says the band has diamonds.
   - With bridge stones on a Pavé band, the DON'T list says the only small stones allowed near
     the centre stone are the bridge stones. That forbids the pavé.
   - Stone seating says the flat top faces "outward"; the next line says "UP toward the ceiling".
   - The opening line asks for a "symmetrical" band on every ring, including Bypass, which must
     not be symmetrical.
   - Rail/Gallery is "a plain metal rail"; the bridge-stones line then describes a second
     bar "under the head" with stones. Gemini gets two rails with no clear place for each.
4. **About 13 DON'T lines name the wrong looks** (split shank, halo, pear, marquise, double
   claws). Naming a look in an image prompt can draw it.
5. **Failed checks become permanent prompt lines** (`src/lessons.js`, up to 10 "Make sure" lines
   per view). When the checker is wrong, its mistake is added to later customers' prompts.
6. **Guide pictures exist for the 3/4 view only, and not all are usable.** The Solitaire band
   tiles are white metal with round stones of about 1 ct (Freddie's correction, Nov 11). Four
   are not at the 3/4 camera and can't be guides as they are: Petite (low front), Double-Row
   Pavé (straight-on front), Baguette Channel (lying on its side) and Bezel Stations (more
   upright). Freddie will check the Three-Stone and Bezel tiles one by one. Some tiles have a
   small band picture in the corner. No look has an approved top-view picture.
7. **Freddie confirmed all six contradictions in point 3** by printing today's prompts. The
   worst is the DON'T line that forbids the pavé stones. He measured 959 words (plain ring, 3/4),
   820 (plain ring, top) and 1,128 (Pavé with bridge stones, 3/4).

### Freddie's numbers (2026-11-11, `nore-freddie/drafts/for-peter-render-fail-stats-2026-11-11.md`)

- **Band is the most-failed check by far:** 31 fails in 201 tile tries. Bridge is next with 8,
  then straight 4 and prongs 3. First-try passes by group: band 13 of 20, look 15 of 27, bridge
  2 of 7; stones, shapes, gemstones and settings pass almost every time.
- **A second try passes only about half the time:** 17 of 33. Tiles pass first try 135 of 168.
- **The checker is wrong in both directions.** Run 30: 6 of 8 fails looked right. Run 38: the
  Tulip passed both views and the owner said it was wrong. The calibration set has 3 pictures.
- **The top view invents extra objects** when it is made from the 3/4 picture (run 39: a second
  head with its own stone; run 37: a hidden-halo look).
- **Never passed a full design:** Diamond Gallery, Tulip petals, the East-West looks. Most new
  band looks have an approved tile but no tested full design.
- **Cost:** $0.154 per image, $0.308 per design. An attached picture adds nothing visible at that
  rounding (not measured exactly).
- **Missing:** fail counts per check and view for real customer designs. Becky's back end has
  them.

## 2. The owner's answers (2026-11-11)

| Question | Answer |
|---|---|
| Rewrite the checker with the prompt? | Yes, both |
| Attach your approved picture as a guide? | Yes, use my pictures |
| What you usually fail | Small stones misplaced; band or shoulders wrong; prongs or head wrong |
| Head faults | Rails thin like wire; tulip petals wrong |
| Start with | All of Hers |
| Pavé band length | About three quarters of the way round |
| Rail thickness | Thicker than a prong |
| Rail/Gallery | Plain metal. Diamond Gallery has the diamonds, low in the gallery |
| Is the Rail/Gallery rail the bridge? | No, two parts. The owner sent a labelled parts diagram (third-party, not stored): the **gallery rail** joins the prongs under the stone; the **bridge** is the bar at the base of the head over the finger opening; a **hidden halo** sits above both, right under the stone's edge |
| Stone size in the render | Keep one size (the guide picture's size; the carat is shown as text) |
| Part names | "fix my wording and refer to the image as that image is the correct terminology" (the labelled diagram) |
| Gallery rail vs gallery | "gallary rail and gallary are two different things" |
| Where Diamond Gallery's diamonds go | "Along the gallery rail", confirmed as "Set into the gallery rail" (both answered in Freddie's chat, relayed by Freddie) |
| What is wrong with the failed Bypass (run 26) | "the bypass design by default is correct its the camera angles that were not consistant with the gemini render if we ask a differetn angle it messes it up" (to Peter, Nov 11) |
| Does that hold for other rings too? | "Bypass only" |

## 3. The method

One owner-approved picture pair (3/4 view and top view) per look, at the standard render cameras.
A customer render is a **short edit of that picture**: the prompt lists only what changes. This
is the Fiorella method (`src/design-refs.js`), which is the only method the owner has passed for a
complex ring.

- A "look" is one setting with one band, e.g. Solitaire + Half Pavé.
- Each view is an edit of **its own** approved picture. The goal is that the top view is no
  longer chained from the 3/4 render (F19: two pictures that disagree made top views worse; runs
  37 and 39: the chained top view invented a second head and a hidden-halo look).
- Still one Gemini call per view. Two tries per view and the $1 cap stay as they are.
- A look with no approved 3/4 picture yet uses today's prompt with the fixes in Part 6.

**Which pictures exist (Freddie, Nov 11):**
- 3/4 view: approved tiles for 16 Solitaire bands (12 at the 3/4 camera; Petite, Double-Row
  Pavé, Baguette Channel and Bezel Stations need a new picture), 10 Three-Stone looks and 9
  Bezel looks (not yet checked one by one). None for East-West, Diamond Gallery or Tulip petals.
- Top view: none. Until a look has an approved top picture, its top view uses prompt 4b with the
  approved 3/4 render of this same ring as the one attached picture (today's chaining, which
  passed 8 of 8 views on the four common rings), plus the "ONE ring with ONE centre stone" line.
- A top picture per look costs about $0.154 each to make, if it passes first try and the owner
  approves it. The run 30 and run 33 top views the owner passes can be the first ones.
- Attaching a look picture to the 3/4 call is possible in the engine (Fiorella does it). The
  call code is Becky's, so the change needs her.

**Two risks Freddie raised (Nov 11). Both are untested and both are in the test plan.**

1. **Stone size: DECIDED, "Keep one size" (owner, Nov 11).** The tiles show about 1 ct and
   customers choose 1 to 10 ct. "Keep the head exactly as in the photo" fights a much bigger
   stone. So every v2 render keeps the guide picture's stone size, as Fiorella does, and the
   carat is not sent to Gemini.
   - The Centre stone line says "at the SAME SIZE as the stone in the photo" (Fiorella's proven
     words). `{CARAT_PROMPT}` is not used in prompts 4a and 4b.
   - The chosen carat stays on the Spec Sheet, the result screen, the emails and the owner alert.
   - `[OWNER + FREDDIE]` the customer should be told the picture shows a standard stone size.
     Fiorella has a note for this; the wording for the normal rings is the owner's to approve.
   - The checker asks nothing about stone size.
   - Not chosen: letting the stone grow with the carat.
2. **Metal.** Fiorella needed its own approved picture per metal. Whether one white-metal tile
   recolours cleanly to yellow or rose is not known. Test it on the first rings; if it fails,
   each look needs one picture per metal colour.

## 4. The prompts

Slots in `{BRACES}` are filled only from the catalogue, by validated id, as today. No customer
text. Lines in `[IF ...]` are left out when the condition is false. Proven lines are reused word
for word: `PROMPT_BASE`, `VIEWS`, `shapeLine`, `facetLine`, `prongLine`, `ORIENTATION` and the
Fiorella edit and keep lines.

### 4a. 3/4 view

```text
{PROMPT_BASE}
Camera: {VIEWS.front}. Keep exactly the camera, framing, lighting and background of the attached photo.
The attached image is NORE's approved photo of this ring style, the {LOOK_NAME}, in {REF_METAL} with {REF_SHAPE_A_AN} centre diamond, seen from the same 3/4 camera angle as this render. This is an EDIT of that photo, not a new design: change ONLY what is listed under "Changes" below, and keep every other part of the ring exactly as it is.
Changes:
[IF METAL DIFFERS]- Metal: {METAL_PROMPT}. Only the colour of the metal changes; the shape of every metal part stays as in the photo.
[IF STONE DIFFERS]- Centre stone: one {GEM_PROMPT}, {SHAPE_PROMPT}, at the SAME SIZE as the stone in the photo.
[IF SHAPE DIFFERS]- {SHAPE_LINE}
[IF SHAPE DIFFERS]- {FACET_LINE}
[IF SHAPE DIFFERS]- {PRONG_LINE}
[IF ELONGATED]- Stone orientation: {ORIENTATION.prompt}. In this view, {ORIENTATION.front}.
[ONE LINE PER BRIDGE CHOICE OR EXTRA THAT THE PHOTO DOES NOT SHOW]- {EXTRA_LINE}
Keep everything else exactly as in the attached photo: the band with its width, weight and height, the way the band meets the head, the head with its rails, and the number and position of every small stone. Do not add, remove, stretch, widen or slim down anything.
Square image. One ring only. No hands, props, boxes, logos or watermark, and no text anywhere.
```

- For a Bypass band, remove the word "symmetrical" from `PROMPT_BASE`.
- No DON'T list and no learned "Make sure" lines in this prompt. Each `{EXTRA_LINE}` carries its
  own single guard (Part 5).
- `{LOOK_NAME}` examples: "Solitaire with a Half Pavé band", "Three-Stone with an Engraved Scroll
  band".
- Lab-grown or natural can't be seen in a picture. `{GEM_PROMPT}` stays as today (colour only),
  and the customer's choice stays on the Spec Sheet, the result screen and the emails. Adding
  the word to the image prompt is a separate test, not part of v2.

### 4b. Top view

```text
{PROMPT_BASE}
Camera: {VIEWS.top}. Keep exactly the camera, framing, lighting and background of the attached photo.
The attached image is NORE's approved photo of this ring style, the {LOOK_NAME}, in {REF_METAL} with {REF_SHAPE_A_AN} centre diamond, seen from the same elevated top-view camera angle as this render. This is an EDIT of that photo, not a new design: change ONLY what is listed under "Changes" below, and keep every other part of the ring exactly as it is.
Changes:
(the same Changes lines as the 3/4 view, with {ORIENTATION.top}, and the top-view wording of each extra from Part 5)
Keep everything else exactly as in the attached photo: the band with its width, weight and height, the way the band meets the head, the head with its rails, and the number and position of every small stone. Do not add, remove, stretch, widen or slim down anything. The picture shows ONE ring with ONE centre stone from this one camera angle.
Square image. One ring only. No hands, props, boxes, logos or watermark, and no text anywhere.
```

- In `VIEWS.top`, the words "with the shoulders sweeping up into the head" are sent only when
  Cathedral arches are chosen.
- **While a look has no approved top picture:** attach the approved 3/4 render of this same ring
  and replace the two lines after `{PROMPT_BASE}` with today's proven pair: `Camera: {VIEWS.top}.`
  and "The attached image is the approved 3/4 view of this exact ring. Show the SAME ring (same
  stone, shape, colour, prongs, setting, band and metal, and the stone pointing the same way
  relative to the band) from the new camera angle above. Change only the camera." Then send no
  Changes list, only the top-view lines of the chosen extras (Part 5), today's hidden-prongs
  line, and the closing lines.

### 4b-2. Bypass: never ask for a camera angle of our own (owner, 2026-11-11)

The owner: "the bypass design by default is correct its the camera angles that were not
consistant with the gemini render if we ask a differetn angle it messes it up".

My reading: Gemini draws a correct Bypass at its own angle (run 25: in the 3/4 picture the stone
sits to one side and tilts toward the camera; in the top picture the ring opening is below the
stone). When the prompt pushes for another angle, the design breaks. `VIEWS.front` says "centre
stone sitting on top of the ring" and `VIEWS.top` says "the opening of the ring ... above and
behind it", so today's camera lines ask for exactly what the approved Bypass does not show.

For a Bypass band, in both views:

- Attach the approved Bypass picture for that view (run 25) as the guide picture.
- Replace the camera line with: `Camera: exactly the camera angle, framing, lighting and
  background of the attached photo. Do not turn, tilt or re-frame the ring.` Do not send
  `{VIEWS.front}` or `{VIEWS.top}`.
- The top view uses run 25's top picture as its guide. It is not made by "Change only the
  camera" from the 3/4 render.
- Checker: on Bypass the camera question (`view`) is note-only, like `seating`. A camera
  difference never fails a Bypass.

New wording, not tested. Scope: the owner answered "Bypass only" (Nov 11). Every other band
keeps its camera line (`{VIEWS.front}`, `{VIEWS.top}`) as written in Parts 4a and 4b.

### 4c. Re-render when a view fails (one retry per view, as today)

The fix line comes from a fixed list, one per check id. It is never the checker's own words.

**Small fault** (a missing or misplaced extra, a wrong colour, an unrequested small stone): edit
the failed picture.

```text
The attached image is the last render of this ring. It is correct except for one thing. Change ONLY this: {FIX_LINE}
Keep everything else exactly as it is: the camera, framing, lighting and background, the metal, the centre stone, the prongs, the head and the band. Do not add, remove or move anything else.
Square image. One ring only. No text anywhere.
```

**Whole-picture fault** (wrong camera, two rings, wrong band, wrong stone shape): render again
from the guide picture with prompt 4a or 4b, and put this line directly after the Camera line:

```text
Correction to the last attempt: {FIX_LINE}
```

Today the corrections go at the very end of a 1,000-word prompt, after the DON'T list.

## 5. Lines for bridge choices and extras

One line each. The guard is the one mistake that option has actually produced.

| Option | 3/4 view line | Top view line |
|---|---|---|
| Rail/Gallery | "Gallery rail: a thick, sturdy plain metal rail that runs round the head and joins the prongs together below the centre stone, about halfway down the prongs and above the bridge; clearly thicker than a prong and close to the thickness of the band, never a thin wire; it has no stones." (The option's name mixes two parts. Its line describes the gallery rail, so the prompt says "gallery rail".) | Leave out (hidden under the stone) |
| Diamond Gallery | **CONFIRMED by the owner twice in Freddie's chat (Nov 11, relayed by Freddie): "Along the gallery rail", then "Set into the gallery rail" over "In the gallery below it".** It is the same rail as Rail/Gallery: Rail/Gallery is that rail in plain metal, Diamond Gallery is that rail with a row of diamonds. Both lines use the same words for the rail. This replaces Peter's earlier reading ("fill the gallery, below the rail"). New line, untested: "Diamond gallery: the gallery rail (the thick, sturdy metal rail that runs round the head and joins the prongs together below the centre stone, about halfway down the prongs and above the bridge, clearly thicker than a prong) is set with one row of small round diamonds all the way round, facing outward and visible from the side. A band of plain metal and open space separates this row from the edge of the centre stone: it is NOT a hidden halo hugging the underside of the stone. The bridge at the base of the head has no stones." **Most likely failure:** Gemini draws it as a hidden halo (run 35 did). A diamond-set gallery rail and a hidden halo differ only by the gap under the stone's edge, so this option needs its own guide picture more than any other. Today's live and branch wording ("LOW down ... between the two shoulders") describes the bridge level and is not reused. | Leave out, and add: "The halo rail, right at the edge of the centre stone, has no stones." |
| Stones on the bridge | Today's line, with its ending changed to "the halo rail (the rail right at the edge of the centre stone) has no stones" and **without** "the shoulders and the band have no stones" when the band has stones. With Rail/Gallery also chosen, add: "The gallery rail above the bridge stays plain metal." The bridge is the bar at the base of the head over the finger opening, below the gallery rail (owner's diagram, Nov 11); today's line already places it there. | Today's top wording: "do not move the stones onto the shoulders or up onto the halo rail... the halo rail has no stones" |
| Tulip petals | Today's line (Freddie's note on run 39 says its 3/4 view matched the owner's photos; the owner hasn't confirmed that to Peter) | Today's `TULIP_TOP_LINE` |
| Cathedral arches | Today's line | Today's `CATHEDRAL_LINE` |
| Two-tone | "The prongs holding the centre stone are bright white gold. This changes their colour only: no prongs are added. The rest of the ring stays {yellow/rose} gold." (one word, "prongs"; "claws" removed) | Same |
| Halo / Hidden halo | Today's setting lines | Hidden halo: leave out |
| Birthstone, Accent colour, Peekaboo, Low/Flat, Filigree | Today's lines | As today |

Band lines change only where the owner gave a new fact:

- **Pavé:** "pavé band: one row of small diamonds set along the top of the band, running about
  three quarters of the way round; the part of the band under the finger is plain polished
  metal." (owner, Nov 11)
- A band line is sent only when the guide picture shows a different band, which should never
  happen when each look has its own picture.

## 6. Fixes to today's prompt (for looks with no guide picture yet)

These remove the contradictions in Part 1. One change at a time, each tested before the next
(Wins & Flops #4).

1. Top-view camera line: send "with the shoulders sweeping up into the head" only with Cathedral
   arches.
2. Bridge stones: drop "the shoulders and the band have no stones" when the band has stones.
3. DON'T line for small stones: list every chosen stone group (band stones included), built from
   the same list as the setting line.
4. Stone seating: one wording, "flat top (table) facing up toward the ceiling".
5. Bypass: remove "symmetrical" from the opening line.
6. Pavé length and rail thickness: the owner's answers above.
7. Learned "Make sure" lines: switch them off until the checker agrees with the owner (Part 7,
   point 3). Freddie's and the owner's call.
8. Part names follow the owner's standard (drafts/jewellery-glossary.md, "NORE's standard part
   names"). In prompts and checks:
   - the label `Bridge:` on the Rail/Gallery, Diamond Gallery, Peekaboo, Filigree/Milgrain and
     Low/Flat lines becomes `Gallery:`. Only "Stones on the bridge" uses the word bridge.
   - the bridge-stones top-view check says the stones sit "low on the bridge", not "low on the
     gallery rail".
   - "rail gallery" becomes "gallery rail".

## 7. Checker v2 (proposal; Freddie calibrates it on pictures the owner has already judged)

1. **Three answers: yes, no, unclear.** Replace "if a detail ... cannot be made out, answer
   false" with "if you can't tell from this angle, answer unclear". Only a clear "no", with the
   visible reason, can fail a view.
2. **Two kinds of question.**
   - **Blocking** (a "no" re-renders the view). These are the things the owner fails:
     - one ring, one centre stone
     - top view taken from above
     - metal colour
     - centre stone colour and shape (exact outline in the top view only)
     - **same build as the guide picture:** "Compared with the FIRST image (NORE's approved photo
       of this ring style), is the SECOND image the same ring apart from the listed changes: the
       same band style and width, the band meeting the head the same way, and rails as thick as
       in the photo? Answer no only if one of these is clearly different."
     - **small stones:** one question per chosen stone group ("is it there, in its place?") and
       one for everything else ("are there no small stones anywhere that were not chosen?")
     - each chosen extra, with the wrong look named ("answer no if only small loops")
   - **Note only** (written in the owner alert, never a re-render): background shade,
     "physically plausible", prong contact, exact prong count in the 3/4 view, facet style,
     reflections, tiny marks.
3. **Calibrate before use.** Replay the new questions (OpenAI only, cents) on every picture the
   owner has already passed or failed. A question that disagrees with the owner is rewritten. No
   Gemini spend.
4. **The calibration set is too small.** It had 3 pictures; since run 41 it has 35 (25 Fiorella,
   only 10 normal rings). Add every picture the owner has passed or failed by eye (run 30, 38, 39
   and the Nov 8 overrides are not in it yet) with the owner's verdict, and keep adding. The
   checker has been wrong both ways: it failed good rings in run 30 and passed a wrong Tulip in
   run 38.
5. **Band and bridge first.** They cause most fails on Freddie's tile data (band 31, bridge 8).
   How many of those band fails were good pictures is not known, so the band question is the
   first one to replay against the owner's verdicts.
6. Fail counts for real customer designs are still missing (Becky has them). The blocking and
   note-only lists above are my proposal until those are in.

### 7a. Checker replay, run 41 (Freddie, 2026-11-11) and the question changes it calls for

Source: `nore-freddie/drafts/checker-replay-run41-2026-11-11.md`. The owner approved it ("Start
checker replay", then "All 35, both checkers", relayed by Freddie). Cost $1.40, no renders.

What was replayed: today's questions with two of my rules added (unclear never fails; note-only
questions never fail). The "same build as the guide picture" question was not replayed, because
there are no guide pictures yet.

| | Today's checker | With the two rules |
|---|---|---|
| Agrees with the owner, all 35 | 29 | 31 |
| Owner's fails caught | 9 of 10 | 9 of 10 |
| Good pictures failed | 5 | 3 |
| Agrees with the owner, 10 normal rings | 7 | 7 |

Plain reading: the two rules fixed two Fiorella pear pictures and broke nothing. On the normal
rings they changed nothing: 7 of 10 before and after. The misses that are left all come from
three pictures of two Bypass rings (runs 25 and 26) and one Fiorella heart (run 19).

The changes below are **new wording, not replayed**. Each one is written for a miss in run 41.
Today's question text is in `nore-freddie/ring-builder/src/spec.js` (`buildChecklist`),
`bands.js` (`bandQuestion`) and `prongs.js` (`prongQuestion`).

**New rule: a chosen feature must be seen.** "Unclear never fails" is right for details the
camera angle hides. It is wrong for the one thing the customer chose that makes the ring
different (the Bypass crossing, the Tulip petals, the Diamond Gallery row). For that feature's
own question, in the view that is meant to show it, unclear counts as no. Without this rule a
ring where the feature is missing can pass as "unclear". Run 41 marked one band answer unclear;
Freddie to say which picture it was.

1. **Camera question (`view`) asks about the camera only.** Today it also asks where the stone
   sits ("centre stone sitting on top of the ring"), and `seating` asks that again, so one doubt
   fails two questions (run 25, 3/4).
   - 3/4 view: "Is this picture taken from a 3/4 angle: the ring stands upright on its band and
     is seen from the front and a little to one side, with the camera slightly above? Judge the
     camera only, not where the stone sits. Answer no only if the camera is clearly different: a
     view from straight above, a flat side-on view with no turn, or a ring lying flat or tipped
     over."
   - Top view: "Is the ring seen from above, with the camera looking down onto the face of the
     centre stone, so the whole outline of the stone can be seen? Judge the camera only. Answer
     no only if this is clearly a side view or a 3/4 view where the top face of the stone is not
     toward the camera. Where the ring opening sits in the picture does not count." (Run 25 top
     failed on "ring opening below the stone"; the owner passed it.)
2. **Stone seating (`seating`), 3/4 view.** Unchanged on every band except Bypass. On Bypass it
   becomes note-only. Reason: on the owner's approved Bypass (run 25) the stone sits to one side
   and tilts toward the camera, which is what the question forbids, and the extra "this is a
   bypass ring" sentence did not stop the fail.
3. **Top-view prongs (`basket`) split in two.**
   - Count, blocking: "Count the prongs holding the CENTRE stone one by one (prongs holding side
     stones, halo or pavé stones do not count). Are there exactly {COUNT}? Answer no if you can
     count a different number." The must-have part (for example the V-shaped prong at a point)
     stays blocking, as today.
   - Exact positions: today's position list as its own question. Note-only on Bypass, where the
     crossing band turns the head (run 25 top: the count was right, the owner passed it, the
     positions failed it). Blocking on every other band until an owner-judged picture shows it is
     too strict. One picture is not enough to loosen it everywhere.
4. **Heart outline at 3/4 (`shape-angle`).** Today's question already allows a hidden cleft, and
   the checker still answered "oval, no cleft" (run 19; the owner passed it). New wording names
   what a clear "no" looks like: "The centre stone should be a heart. From this angle the cleft
   and the point may both be hidden. Answer no only if you can clearly see a shape that cannot
   be a heart: straight sides with square or cut corners, or a point at both ends. If you see a
   rounded outline and can't tell, answer unclear." The exact outline stays blocking in the top
   view.
5. **Bypass band (`band`): the crossing must be seen.** Today's question does name the wrong
   look, but its last sentence ("answer false only if the band is clearly symmetrical") lets a
   bent solitaire pass (run 26; the owner: "a messed up solitare"). New wording: "Look at where
   the band meets the centre stone. On a bypass ring the band's two ends do not meet: one end
   stops on one side of the stone, the other end stops on the other side, and they pass each
   other. Can you see the two ends passing each other? Answer no if both sides of the band run
   into the head the way a solitaire band does, even if the band is bent, uneven or tilted."
   The "must be seen" rule applies. Every other special band and every extra gets the same
   treatment: its wrong look is named, as already listed above for the Tulip.

**Test for these five changes (cents, no renders, needs the owner's yes):** replay the same 35
pictures. They pass if: run 25 3/4 and run 25 top now pass; run 19 heart 3/4 passes; run 26 fails
in both views; and no answer that agreed with the owner in run 41 flips. If the new Bypass
question can't tell run 25 from run 26, the Bypass needs the guide-picture question instead,
with run 25's approved pictures as the guide.

Limit, said before the spend: these questions were written after seeing these same pictures, so
passing this replay shows only that the wording is no longer wrong on them. The real proof is
pictures the owner judges from now on.

Naming note for Freddie: `ring-builder/src/prompt-v2.js` is my older normal template v1.1 (Nov
10). It is not this document. This document's prompts are in Part 4.

### 7b. Exact strings for the second replay (sent to Freddie, 2026-11-11)

The owner said "yes to all" to Freddie's list of next steps (relayed by Freddie, Nov 11): Peter
updates the questions, then a short re-check; Becky's change to attach the approved picture; the
8 test rings, better in December's budget. The strings below are written in the engine's
true/false form. `{...}` is a value the code already has. Still new wording, not replayed.

- **`view`, 3/4 view** (replaces `'Is the camera angle a ' + viewText + '?'`; no Bypass
  sentence added):
  `Is this picture taken from a 3/4 angle: the ring stands upright on its band and is seen from the front and a little to one side, with the camera slightly above? Judge the camera only, not where the centre stone sits. Answer false only if the camera is clearly different: a view from straight above, a flat side-on view with no turn, or a ring lying flat or tipped over.`
- **`view`, top view** (same; no Bypass sentence added):
  `Is the ring seen from above, with the camera looking down onto the face of the centre stone, so the whole outline of the stone can be seen? Judge the camera only. Answer false only if this is clearly a side view or a 3/4 view where the top face of the stone is not toward the camera. Where the ring opening sits in the picture does not count.`
- **`seating`**: text unchanged. On `band:bypass` it is note-only.
- **`basket-count`, top view, blocking** (first half of today's `prongQuestion`):
  `Count the prongs holding the CENTRE stone one by one (prongs holding side stones, halo or pavé stones do not count). Are there exactly {N pairs of claws (T tips) | N single prongs}? Answer false if you can clearly count a different number{, or if any prong is a double claw | nothing for pairs}{, or if {mustHave} is missing | nothing}.`
- **`basket-positions`, top view** (second half of today's `prongQuestion`). Note-only on
  `band:bypass`; blocking on every other band:
  `Look at the prongs holding the CENTRE stone. Is there one at EVERY one of these positions: {positions joined with "; "}? Answer false if any position has no prong.`
- **`shape-angle`, heart only, 3/4 view** (in `buildChecklist` and `buildDesignChecklist`; other
  shapes keep today's text):
  `The centre stone should be a heart. From this angle the cleft and the point may both be hidden. Answer false only if you can clearly see a shape that cannot be a heart: straight sides with square or cut corners, or a point at both ends. If you see a rounded outline and cannot tell, it is unclear, not false.`
- **`band`, `band:bypass`, both views** (replaces `bandQuestion` plus the `BYPASS_FAIR.band`
  sentence). "Must be seen": unclear counts as false for this question:
  `Look at where the band meets the centre stone. On a bypass ring the two ends of the band do not meet: one end stops on one side of the stone, the other end stops on the other side, and they pass each other. Can you see the two ends passing each other? Answer false if both sides of the band run into the head the way a solitaire or cathedral band does, even if the band is bent, uneven or tilted. Also answer false if it is a split shank (one end dividing into two strands) or a twisted rope band.`

One difference from Freddie's list: his says prong positions note-only; mine says note-only on
Bypass only. The replay should record the positions answer on every top-view picture, so the
owner's verdicts show which is right.

### 7c. Second replay, run 42 (Freddie, 2026-11-11): what held and what did not

Run 42: the 7b wording on the same 35 pictures, one checker, $0.70 (covered by the owner's "yes
to all", relayed by Freddie). Report: `nore-freddie/ring-builder/review/calibration-report-v2b.json`.

| My pass test | Result |
|---|---|
| Run 19 heart 3/4 passes | Yes |
| Run 26 fails in both views | Yes ("both sides run into the head") |
| Run 25 3/4 and top pass | **No.** Both failed on my new Bypass band question |
| Nothing that agreed in run 41 flips | 3 flips: one was a scope bug in the script (fixed by Freddie), two were the white pear 3/4 pictures |

Total: 30 of 35 as run, 31 of 35 with Freddie's scope fix. Run 41 was 31 of 35. So the rewording
moved the misses; it did not reduce them.

What I take from it:

1. **Words alone can't tell the approved Bypass from the failed one.** Today's question passes
   both; my 7b question fails both. Item 7 in 7b is withdrawn. The Bypass band is judged by
   comparing with the approved picture (below).
2. **The run 41 "unclear" band answer was on run 25 3/4** (the approved ring), not run 26. So
   the unclear rule did not cause run 26's false pass; the old wording did.
3. **The pear at 3/4 is unstable.** The same unchanged question said "unclear" in run 41 and
   "oval, no point" in run 42 on the same two pictures. A single answer on a borderline picture
   is not reliable.
4. **"A chosen feature must be seen" applies in one view only:** the view meant to show that
   feature (3/4 for most). Applied in the top view too, it failed a good picture (run 22).
5. Items 1 to 6 of 7b stand: camera-only `view`, Bypass `seating` as a note, the prong split,
   and the heart wording did what they were written for.

**Bypass band, guide-picture question (replaces 7b item 7; new wording, not replayed).** Two
pictures go to the checker: FIRST, the owner-approved Bypass at the same view (run 25:
`nb-bypass-white-oval-v2-front-1.png` for the 3/4 view, `nb-bypass-white-oval-v2-top-1.png` for
the top view); SECOND, the render being checked. Blocking, and unclear counts as false.

`The FIRST image is NORE's approved bypass ring, seen from the same camera angle. The SECOND image is the ring being checked. Ignore the metal colour and the centre stone's shape, colour and size. Look only at how the band and the centre stone are built together. In the FIRST image the centre stone sits low, held between the two ends of the band: one end of the band arrives at one end of the stone and the other end arrives at the opposite end, so the stone lies between them. Is the SECOND image built the same way? Answer false if in the SECOND image the stone stands on a raised head above the band, or if the band curls underneath or behind the stone as one continuous loop, or if both sides of the band rise evenly to the head like a solitaire.`

Limits, said before any spend:
- The description of the two builds is mine, from looking at run 25 and run 26. The owner did
  not confirm it. Asked what is wrong with run 26, he named the cause instead: "the bypass
  design by default is correct its the camera angles that were not consistant with the gemini
  render if we ask a differetn angle it messes it up" (Nov 11). So the first fix is in the
  render prompt (Part 4b-2: never ask for our own camera angle on a Bypass), and this check is
  the backstop. Its "answer false if ..." list stays my own reading until a second owner-judged
  Bypass exists.
- It can be tested on run 26 only (2 pictures, a few cents). Run 25 can't be tested against
  itself. Run 25 is the only Bypass the owner has passed, so this question can't be proven until
  the owner passes a second Bypass.

**Pear at 3/4 (`shape-angle`, pear only; other shapes keep today's text; new wording, not
replayed):**

`The centre stone should be a pear: one rounded end and one pointed end. From this angle the point may be hidden or look shorter. Answer false only if you can clearly see a shape that cannot be a pear: straight sides with square or cut corners, a point at both ends, or a cleft. If you see a rounded outline and cannot tell, it is unclear, not false.`

If the pear still flips between runs with this wording, the 3/4 shape question becomes note-only
for pear, heart and marquise, and the exact outline is judged in the top view only.

A third replay (the pear pictures and the run 26 pair, or all 35 at about $0.70) needs a new yes
from the owner. Run 42 used the "short re-check" he approved. Freddie will not spend on a third
replay now: the guide-picture question needs Becky's checker change first (the guide picture
passed to the check), and he will propose its test to the owner together with the December test
rings.

Prong positions, from run 42's report: the positions question was recorded on every top view.
It disagreed only on the two Bypass top views (runs 25 and 26). On the other top views in the
set it agreed with the owner while still blocking. So "note-only on Bypass only" stays.

## 8. Test plan (each step needs the owner's yes)

1. Checker replay on judged pictures. Cents, no Gemini. **First replay done: run 41, $1.40
   (Part 7a).** A second replay of the five reworded questions is the next cheap step.
2. The owner picks or approves the guide pair for 8 looks.
3. Render 8 rings that fail today with prompts 4a and 4b, one try per view. About $0.31 each,
   about $2.48 if all pass first time, $8.00 at most under the $1 cap. Suggested set: Solitaire
   Half Pavé (pear, yellow); Solitaire Plain + Stones on the bridge (round, rose); Solitaire Plain
   + Tulip petals (oval, yellow); Solitaire Plain + Diamond Gallery (round, white); Solitaire Pavé
   + Cathedral + Two-tone (marquise, yellow); Three-Stone Engraved (emerald cut, platinum); Bezel
   + Bezel Stations (oval, white); East-West Plain (oval, rose).
4. The owner judges all 16 pictures by eye. Peter logs the result as a WIN or FLOP in the
   owner's words.
5. Only then: extend look by look.

## 9. Open items

| Item | Who |
|---|---|
| Rail/Gallery rail and bridge | ANSWERED by the owner's labelled diagram (Nov 11): "that image is the correct terminology"; "gallary rail and gallary are two different things" |
| Customer-facing names: rename the step "Choose the bridge" (it holds gallery choices) and the option "Rail/Gallery" (it joins two parts) to match the standard names | Owner decides, Freddie applies |
| Today's code and check questions call the bridge "the gallery rail" in places (for example the bridge-stones top-view check). Those words now name the wrong part | Freddie |
| Second checker replay with the reworded questions | DONE: run 42, $0.70 (Part 7c) |
| Which picture had the "unclear" band answer in run 41 | ANSWERED: run 25 3/4 (Freddie) |
| Checker change: pass the guide picture to the check, for the Bypass guide question (Part 7c) and the "same build as the guide" question (Part 7) | Becky, with the owner's approval |
| Test of the Bypass guide question and the pear wording (cents) | Owner approves; Freddie proposes it with the December test rings |
| What exactly is wrong with run 26 in the owner's eyes | ANSWERED (Nov 11): the camera angle asked for, not the Bypass design. See Part 4b-2 |
| Does "asking for a different angle messes it up" hold for Bypass only, or for other rings too | ANSWERED (Nov 11): "Bypass only" |
| Fail counts per check and per view for real customer designs (counts only, no customer rows) | Becky |
| Engine change: attach the look's picture to the 3/4 call | Becky, with the owner's approval |
| Check each tile before it is a guide picture (camera angle, no corner picture) | Freddie |
| Approved top-view picture per look; guide pictures for East-West, Diamond Gallery and Tulip petals | Owner approves, Freddie renders |
| Do the metals need their own guide picture each (Fiorella did), or does one white-metal pair hold | Test |
| Customer-facing note that the render shows a standard stone size (wording) | Owner, with Freddie |
| Rail thickness "thicker than a prong": Freddie changes his Rail/Gallery line once the owner confirms it to him | Owner, then Freddie |
| Fix the six contradictions in today's prompt now, or wait for v2 | DECIDED: the owner chose "Wait for Peter's v2" (relayed by Freddie, Nov 11). Today's prompts stay as they are; the Part 6 fixes go in with v2, once approved |
| Stone origin of accent and bridge stones; birthstone place with bridge stones; `[OWNER CHECK]` lines in the glossary | Owner (from earlier) |
