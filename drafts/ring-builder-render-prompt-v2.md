# Ring builder render prompt v2 (Hers): guide picture + short edit

- From: Peter (nore-prompter), 2026-11-11. For: the owner, then Freddie (nore-freddie).
- Status: **DRAFT, NOT TESTED.** Nothing here is live. Freddie applies it only with the owner's
  approval; every test render needs the owner's approval of that spend.
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
| Where Diamond Gallery's diamonds go | "Along the gallery rail" (answered in Freddie's chat, relayed by Freddie) |

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
| Diamond Gallery | **Owner, relayed by Freddie (Nov 11): "Along the gallery rail".** The diamonds are a row set into the gallery rail itself. This replaces Peter's earlier reading ("fill the gallery, below the rail"). New line, untested: "Diamond gallery: the gallery rail (the thick, solid metal rail that runs round the head and joins the prongs together below the centre stone, about halfway down the prongs) is set with one row of small round diamonds all the way round, facing outward and visible from the side. A band of plain metal and open space separates this row from the edge of the centre stone: it is NOT a hidden halo hugging the underside of the stone. The bridge at the base of the head has no stones." **Most likely failure:** Gemini draws it as a hidden halo (run 35 did). A diamond-set gallery rail and a hidden halo differ only by the gap under the stone's edge, so this option needs its own guide picture more than any other. Today's live and branch wording ("LOW down ... between the two shoulders") describes the bridge level and is not reused. | Leave out, and add: "The halo rail, right at the edge of the centre stone, has no stones." |
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
4. **The calibration set is too small.** It has 3 pictures. Add every picture the owner has
   passed or failed by eye (run 22, 25, 26, 30, 38, 39 and the Nov 8 overrides) with the owner's
   verdict, and keep adding. The checker has been wrong both ways: it failed good rings in run 30
   and passed a wrong Tulip in run 38.
5. **Band and bridge first.** They cause most fails on Freddie's tile data (band 31, bridge 8).
   How many of those band fails were good pictures is not known, so the band question is the
   first one to replay against the owner's verdicts.
6. Fail counts for real customer designs are still missing (Becky has them). The blocking and
   note-only lists above are my proposal until those are in.

## 8. Test plan (each step needs the owner's yes)

1. Checker replay on judged pictures. Cents, no Gemini.
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
| Fail counts per check and per view for real customer designs (counts only, no customer rows) | Becky |
| Engine change: attach the look's picture to the 3/4 call | Becky, with the owner's approval |
| Check each tile before it is a guide picture (camera angle, no corner picture) | Freddie |
| Approved top-view picture per look; guide pictures for East-West, Diamond Gallery and Tulip petals | Owner approves, Freddie renders |
| Do the metals need their own guide picture each (Fiorella did), or does one white-metal pair hold | Test |
| Customer-facing note that the render shows a standard stone size (wording) | Owner, with Freddie |
| Rail thickness "thicker than a prong": Freddie changes his Rail/Gallery line once the owner confirms it to him | Owner, then Freddie |
| Fix the six contradictions in today's prompt now, or wait for v2 | DECIDED: the owner chose "Wait for Peter's v2" (relayed by Freddie, Nov 11). Today's prompts stay as they are; the Part 6 fixes go in with v2, once approved |
| Stone origin of accent and bridge stones; birthstone place with bridge stones; `[OWNER CHECK]` lines in the glossary | Owner (from earlier) |
