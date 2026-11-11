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
6. **The tile pictures are not at the render camera.** They are round stones in white metal at
   mixed angles (Petite and Double-Row Pavé are low or face-on, Baguette Channel lies down). They
   can't be used as guide pictures as they are.

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
| Is the Rail/Gallery rail the bridge? | No, two parts. **The owner will send a marked photo** |

## 3. The method

One owner-approved picture pair (3/4 view and top view) per look, at the standard render cameras.
A customer render is a **short edit of that picture**: the prompt lists only what changes. This
is the Fiorella method (`src/design-refs.js`), which is the only method the owner has passed for a
complex ring.

- A "look" is one setting with one band, e.g. Solitaire + Half Pavé.
- Each view is an edit of **its own** approved picture. The top view is not chained from the 3/4
  render (F19: two pictures that disagree made top views worse).
- Still one Gemini call per view. Two tries per view and the $1 cap stay as they are.
- A look with no approved pair yet uses today's prompt with the fixes in Part 6.

**`[FREDDIE TO CONFIRM]`** which approved pairs exist. The run 30 and run 33 test renders
(`review/gallery-tests/ss-*-white-oval-front-1.png` and `-top-1.png`) are at the right cameras.
The ones the owner passes can be the first guide pictures. Missing looks need one approved pair
each (about $0.31 per look if it passes first try).

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
[IF STONE DIFFERS]- Centre stone: one {GEM_PROMPT}, {SHAPE_PROMPT}, {CARAT_PROMPT}.
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
| Rail/Gallery | `[OWNER PHOTO NEEDED: where this rail sits]` ... a thick, sturdy plain metal rail, clearly thicker than a prong and close to the thickness of the band, never a thin wire | Leave out (hidden under the stone) |
| Diamond Gallery | Today's line, unchanged (owner confirmed it has diamonds, low in the gallery) | Leave out, and add: "The halo rail, right at the edge of the centre stone, has no stones." |
| Stones on the bridge | Today's line, with its ending changed to "the halo rail (the rail right at the edge of the centre stone) has no stones" and **without** "the shoulders and the band have no stones" when the band has stones. `[OWNER PHOTO NEEDED: bridge vs Rail/Gallery rail]` | Today's top wording: "do not move the stones onto the shoulders or up onto the halo rail... the halo rail has no stones" |
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
4. **`[FREDDIE'S DATA NEEDED]`** fail counts per check id, to confirm which checks cause the
   false fails. The blocking and note-only lists above are my proposal until then.

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
| Marked photo: Rail/Gallery rail and bridge | Owner |
| Which approved picture pairs exist; cost of a call with one attached picture; whether the engine can attach a look picture to the 3/4 call | Freddie |
| Fail counts per check and per view | Freddie |
| Do the metals need their own guide picture each (Fiorella did), or does one white-metal pair hold | Test |
| Stone origin of accent and bridge stones; birthstone place with bridge stones; `[OWNER CHECK]` lines in the glossary | Owner (from earlier) |
