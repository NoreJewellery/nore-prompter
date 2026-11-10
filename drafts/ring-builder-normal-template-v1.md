# Ring builder render template, normal settings, with Extras: proposal v1

- From: Peter (nore-prompter), 2026-11-10. For: Freddie (nore-freddie).
- Status: PROPOSAL. Not tested. Freddie tests it against the current prompt on the same rings;
  the owner approves any change and any render spend.
- Scope: normal builder settings only. Not Fiorella.
- Sources: `nore-freddie/drafts/builder-prompt-for-review.md` and `render-notes-nov-10.md`.

## What changed and why

1. **Proven order kept:** base style, then camera, then reference (top view only), then the ring,
   then avoid lines. The camera stays second.
2. **Every fact is said once.** Today the claw count appears 3 times and the band form 4 times.
   Here each part has one line, and pose and seating move into the camera block.
3. **One complete stone list replaces the scattered "only small stones are..." text.** The code
   builds it from catalogue values. It is the single place that says which stones exist, so the
   setting, band and avoid lines never have to list stones (that is where today's
   contradictions 1 and 2 came from).
4. **Bridge stones take their colour from the accent colour.** The prompt calls them "bridge
   stones", not "diamonds". Their material word is `{ACCENT_STONE}`: colourless diamonds by
   default, or the chosen accent colour. This fixes contradiction 2.
5. **The band line is scoped when bridge stones are on.** "No stones" applies to the band
   itself, and the pavé/stone warnings drop out. This fixes contradictions 1 and 5.
6. **Two-tone claws change colour only.** The claw colour sits in the Metal line, which says the
   claws are the same set described under Prongs, with none added. There is also one avoid line
   against white claws added next to metal ones. This targets the extra claws on the pear and the
   marquise. It is a hypothesis, so test it on those two rings first.
7. **Avoid lines are conditional.** Each line is included only when its condition is true, so no
   avoid line can contradict a choice. The general "do not add anything not listed" line appears
   once, replacing contradiction 3.
8. **The birthstone line changes per view.** In the 3/4 view it is visible from the side. In the
   top view the centre stone covers it, and the prompt says not to move or enlarge it to show it.
   (Otherwise Gemini may "help" by bringing it into view.)
9. **Target length:** about 450–600 words per view once the lines are filled in (today: 1,148 and
   1,087).

## Slots (catalogue values only, no customer free text)

| Slot | Source | Example (design 10) |
|---|---|---|
| `{RING_FOR}` | catalogue | women's ring |
| `{METAL_LINE}` | metal catalogue line | 14 karat rose gold (warm pink) |
| `{STONE_ORIGIN}` | catalogue: `lab-grown` / `natural` | lab-grown |
| `{STONE_LINE}` | gemstone catalogue line | colourless white diamond |
| `{SHAPE}` | shape | oval |
| `{CARAT}` | carat pick list | 1.50 |
| `{SHAPE_OUTLINE_LINE}` | per-shape line | The outline is an elongated ellipse with two rounded ends and no points. |
| `{FACET_LINE}` | per-shape line | It has brilliant faceting: many small triangular and kite-shaped facets that sparkle. |
| `{SHAPE_NOT_LINE}` | per-shape line | a pointed end (pear), two pointed ends (marquise), or a round outline |
| `{ORIENTATION_3Q}` / `{ORIENTATION_TOP}` | elongated shapes only | see template |
| `{SETTING_LINE}` | setting catalogue line, **structure only, no stone list** | solitaire setting: one centre stone, no halo |
| `{PRONG_COUNT}` | basket | four |
| `{PRONG_LAYOUT_LINE}` | per basket x shape line | Exactly four claw prongs, evenly spaced like the four corners of a square, none missing and none extra. |
| `{BRIDGE_LINE}` | bridge catalogue line | see below |
| `{BAND_LINE}` | band catalogue line, **two variants: with or without bridge stones** | see below |
| `{ACCENT_STONE}` | accent colour extra, else default | rich green emerald / colourless diamond |
| `{BRIDGE_STONES_LINE}` | bridge-stones extra (option A or B, owner to choose) | see Part 2 |
| `{BIRTHSTONE}` | birthstone extra (month to stone) | pink tourmaline |
| `{SETTING_ACCENTS}` | setting's own accent stones, if any (halo, side, pavé) | (none for a solitaire) |

The pre-render check can keep checking that each catalogue line appears. The stone list is
built from those same lines, so it can be checked the same way.

---

## Part 1a: 3/4 view template

```text
Macro commercial jewellery studio photograph of one fine-jewellery ring: photorealistic, seamless pure white background, soft softbox lighting with realistic metal reflections and gemstone brilliance, razor-sharp focus, 100mm macro lens. Accuracy matters more than artistic flair: render exactly the ring described below, with crisp individual prongs, realistic faceting and a clean, symmetrical, physically sound band.

Camera: 3/4 view. The ring stands upright on the bottom of its band, turned about 30 to 45 degrees, with the camera slightly above. The centre stone is at the very top of the ring, seated down in its setting with its flat top (table) facing up toward the ceiling; it is never stood on its point, put on the side of the ring nearest the camera, or tilted to face the camera.

The ring (each part is described once; render exactly this):
- Ring for: {RING_FOR}.
- Metal: {METAL_LINE}, for the whole ring.[IF TWO-TONE] The one exception is the claws holding the centre stone, which are bright white gold. This changes their colour only: they are the same claws described under Prongs, and no claws are added.[/IF]
- Centre stone: one {STONE_ORIGIN} {STONE_LINE}, {SHAPE} cut, about {CARAT} carat, in realistic proportion to the band. {SHAPE_OUTLINE_LINE} {FACET_LINE}
[IF ELONGATED]- Orientation: north-south: the stone's long axis runs along the finger, at a right angle to the band. In this view the stone's length points toward and away from the camera, not along the curve of the band.[/IF]
- Setting: {SETTING_LINE}.
- Prongs: {PRONG_LAYOUT_LINE} Each prong is one single claw that visibly touches and grips the edge of the centre stone.
- Bridge: {BRIDGE_LINE}
- Band: {BAND_LINE}
- Stones: this is the complete list of stones on the ring. There are no others anywhere.
  - the centre stone
  [IF SETTING ACCENTS]- {SETTING_ACCENTS}, all {ACCENT_STONE}[/IF]
  [IF BRIDGE STONES]- {BRIDGE_STONES_LINE}[/IF]
  [IF BIRTHSTONE]- one small round {BIRTHSTONE} set in the gallery directly under the centre stone, visible from the side; it is the only stone in the gallery[/IF]

Square image. One ring only. No hands, props, boxes, logos, watermark or text.

Avoid:
- adding any stone, halo, milgrain, prong or other detail that is not described above.
[IF ELONGATED OR FANCY]- drawing the centre stone with {SHAPE_NOT_LINE}.[/IF]
[IF BRILLIANT FACETS]- long parallel step facets (an emerald-cut look) in the centre stone.[/IF]
[IF TWO-TONE]- adding white claws beside metal-coloured ones: there is one set of claws, and all of them are white gold.[/IF]
[IF PLAIN BAND]- a split shank, a twisted band, or two strips of metal side by side or a gap running along the band on either side of the stone.[/IF]
[IF CATHEDRAL]- an open window or hole between the band and the head: each arch is the band itself curving up in one solid piece.[/IF]
[IF PLAIN BAND AND NO BRIDGE STONES]- stones on the band or shoulders.[/IF]
```

## Part 1b: top view template (approved 3/4 image attached)

```text
Macro commercial jewellery studio photograph of one fine-jewellery ring: photorealistic, seamless pure white background, soft softbox lighting with realistic metal reflections and gemstone brilliance, razor-sharp focus, 100mm macro lens. Accuracy matters more than artistic flair: render exactly the ring described below, with crisp individual prongs, realistic faceting and a clean, symmetrical, physically sound band.

Camera: elevated top view. The ring stands upright; the camera is above and in front of it, about 35 to 45 degrees from straight down, looking onto the face of the centre stone. The stone sits in the lower part of the picture; the ring's opening and the far side of the band are seen above and behind it, with the shoulders sweeping up into the head. The shot is not flat from straight above and not from a low side angle.

Reference: the attached image is the approved 3/4 view of this exact ring. Show the same ring (same stone, shape, colour, setting, prongs, bridge, band and metal, and the stone pointing the same way relative to the band) from this new camera angle. Change only the camera. Some prongs are hidden behind the stone in the reference: draw every prong described under Prongs, not only the ones visible there.

The ring (each part is described once; render exactly this):
- Ring for: {RING_FOR}.
- Metal: {METAL_LINE}, for the whole ring.[IF TWO-TONE] The one exception is the claws holding the centre stone, which are bright white gold. This changes their colour only: they are the same claws described under Prongs, and no claws are added.[/IF]
- Centre stone: one {STONE_ORIGIN} {STONE_LINE}, {SHAPE} cut, about {CARAT} carat, in realistic proportion to the band. {SHAPE_OUTLINE_LINE} {FACET_LINE}
[IF ELONGATED]- Orientation: north-south: the stone's long axis runs along the finger, at a right angle to the band. In this view the stone's long axis crosses the band at a right angle.[/IF]
- Setting: {SETTING_LINE}.
- Prongs: {PRONG_LAYOUT_LINE} Each prong is one single claw that visibly touches and grips the edge of the centre stone.
- Bridge: {BRIDGE_LINE}
- Band: {BAND_LINE}
- Stones: this is the complete list of stones on the ring. There are no others anywhere.
  - the centre stone
  [IF SETTING ACCENTS]- {SETTING_ACCENTS}, all {ACCENT_STONE}[/IF]
  [IF BRIDGE STONES]- {BRIDGE_STONES_LINE}[/IF]
  [IF BIRTHSTONE]- one small round {BIRTHSTONE} set in the gallery directly under the centre stone. From this angle the centre stone covers it: do not move it, enlarge it or add another to make it visible.[/IF]

Square image. One ring only. No hands, props, boxes, logos, watermark or text.

Avoid:
- adding any stone, halo, milgrain, prong or other detail that is not described above.
- large bright white glare patches on the band or shoulders; keep metal reflections soft and even.
[IF ELONGATED OR FANCY]- drawing the centre stone with {SHAPE_NOT_LINE}.[/IF]
[IF BRILLIANT FACETS]- long parallel step facets (an emerald-cut look) in the centre stone.[/IF]
[IF TWO-TONE]- adding white claws beside metal-coloured ones: there is one set of claws, and all of them are white gold.[/IF]
[IF PLAIN BAND]- a split shank, a twisted band, or two strips of metal side by side or a gap running along the band on either side of the stone.[/IF]
[IF CATHEDRAL]- an open window or hole between the band and the head: each arch is the band itself curving up in one solid piece.[/IF]
[IF PLAIN BAND AND NO BRIDGE STONES]- stones on the band or shoulders.[/IF]
```

## Catalogue lines this template needs

- **Bridge, Cathedral:** "cathedral bridge: on each side the band itself sweeps up in one smooth,
  solid arch to lift and hold the head; seen from above, each shoulder widens and rises into the
  head as one piece, never as a second strip beside the band."
- **Band, Plain, no bridge stones:** "plain polished metal band with no stones: one continuous
  strip all the way round that does not divide near the stone. Seen from above it is exactly one
  strip of metal on each side of the stone (the far side seen behind the stone is the same band)."
- **Band, Plain, with bridge stones:** under option A: "plain polished metal band: one continuous
  strip all the way round that does not divide near the stone, with no stones set in the band
  itself (the bridge stones sit on the arches only). Seen from above it is exactly one strip of
  metal on each side of the stone." Under option B, replace the bracket with "(the only stones
  near it are the shoulder stones described under Stones)".
- **Setting lines** must describe structure only. For example, the solitaire line should stop at
  "one centre stone, no halo, no side stones on the band". The stone list carries the extras.
- **Prong layout lines** are per basket x shape. Please send me the pear (5-prong / V-prong) and
  marquise lines. The V-prong at a pear's point must count as **one** claw in both the prompt and
  the check, or "five" and the picture will disagree. I haven't seen those lines yet.

---

## Part 2: bridge stones, options for the owner

The owner chooses which ring NORE actually sells. That choice decides the wording; ease of
rendering should not. Today's fails were caused by our rules, not by Gemini: by eye, all three
renders showed bridge stones.

**Option A: on the arches only (closest to the name "on the bridge")**
> a single row of small round {ACCENT_STONE} stones set along the top edge of each cathedral
> arch, on both sides of the head, running from the head down to where the arch meets the band;
> the band itself has no stones.
- For: matches the extra's name, and the band stays plain, so the band checks barely change.
- Against: Gemini drifted down the shoulders 3 times out of 3, so the first-try pass rate may
  drop. Test it before choosing.

**Option B: down the shoulders (what Gemini drew on its own)**
> a single row of small round {ACCENT_STONE} stones set along the top of the band on each
> shoulder, starting at the head and running about [SHOULDER LENGTH, e.g. one third] of the way
> down the band on each side; the rest of the band is plain polished metal.
- For: likely the highest first-try pass rate, because it matches Gemini's habit.
- Against: it is a different product (pavé shoulders, not a jewelled bridge). The owner and CAD
  must confirm they make and price it this way, and how far the stones run.
  `[SHOULDER LENGTH]` is the owner's call; don't guess it.

**If the owner wants both (arch plus shoulders):** treat that as option B with the arch included
and name it clearly. Do not blend A and B wording in one line.

Either way: say where the row starts and where it stops, use one row (not "pavé"), and take the
colour from `{ACCENT_STONE}`. The extra stays Cathedral-only.

---

## Part 3: check questions to change

| Check | Change |
|---|---|
| `setting` | Build it from `{SETTING_LINE}` only (structure), with no stone list. |
| `band` | Use the band-line variant that matches the prompt. With bridge stones, ask: "Is the band itself one plain polished strip all the way round, with no stones set in it [A: below the arches / B: beyond the stone-set shoulders], not split, not twisted?" |
| `nothing-extra` | Replace the long dump with the stone list: "Apart from these stones: [stone list], are there no other stones, no halo, no milgrain, no extra prongs and no text on the ring?" |
| `extra-bridgeDiamonds` | Rename to `extra-bridgeStones`. "Is there a row of small {ACCENT_STONE} stones [A: along the top of each cathedral arch / B: along each shoulder from the head], on both sides?" **Add it to the top view too**: bridge stones show from above and the check is missing there today. |
| `extra-twoToneClaws` | Add the count: "Are the claws holding the centre stone white metal, with the rest of the ring {METAL_COLOUR}, and is there only one set of claws (no white claws added beside metal ones)?" The top-view `basket` count also catches extra claws. |
| `extra-accentColour` | Name the accent stones on this ring: "Are the [bridge stones / halo stones / ...] {ACCENT_STONE}?" Then it can't fail a ring for accents it doesn't have. |
| `extra-birthstone` (top view) | Keep it out of the top view. If you want a guard, add: "If a small {BIRTHSTONE} is visible, is it under the centre stone and is there only one?" |
| `basket` / `basket-angle` | Use the same `{PRONG_LAYOUT_LINE}` as the prompt; for the pear, count the V-prong as one. |
| `shape-angle`, `view` | Grammar: "a oval" → "an oval" and "a elevated" → "an elevated" (choose a/an from the slot). |

---

## Flags (please read)

1. **"Concept render" label:** NORE's rule is that public render images carry the on-image label
   "Concept render". The Gemini prompt correctly says "no text", so the label has to be overlaid
   by the code after approval. Please confirm the code does this. If it doesn't, that's a gap to
   raise with the owner. Don't ask Gemini to draw the label.
2. **Lab-grown / natural:** my rules say prompts must state lab-grown or natural exactly, so
   `{STONE_ORIGIN}` is in the stone line. It shouldn't change the look; please confirm on a test
   ring that it doesn't. Owner question: do accent and bridge stones follow the centre stone's
   origin, or are they always one kind? Until the owner answers, `{ACCENT_STONE}` carries no
   origin word.
3. **The avoid lines** are the conditional ones above. Keep any other "DON'T" from today's file
   only where you have render evidence for it.
4. **Owner decisions still open:** bridge stones option A or B (and `[SHOULDER LENGTH]` for B);
   accent stone origin; whether the customer-facing name stays "Diamonds on the bridge" when the
   stones can be emeralds.

## Filled example: design 10, option A (to compare against today's prompt)

```text
Macro commercial jewellery studio photograph of one fine-jewellery ring: photorealistic, seamless pure white background, soft softbox lighting with realistic metal reflections and gemstone brilliance, razor-sharp focus, 100mm macro lens. Accuracy matters more than artistic flair: render exactly the ring described below, with crisp individual prongs, realistic faceting and a clean, symmetrical, physically sound band.

Camera: 3/4 view. The ring stands upright on the bottom of its band, turned about 30 to 45 degrees, with the camera slightly above. The centre stone is at the very top of the ring, seated down in its setting with its flat top (table) facing up toward the ceiling; it is never stood on its point, put on the side of the ring nearest the camera, or tilted to face the camera.

The ring (each part is described once; render exactly this):
- Ring for: women's ring.
- Metal: 14 karat rose gold (warm pink), for the whole ring. The one exception is the claws holding the centre stone, which are bright white gold. This changes their colour only: they are the same claws described under Prongs, and no claws are added.
- Centre stone: one lab-grown colourless white diamond, oval cut, about 1.50 carat, in realistic proportion to the band. The outline is an elongated ellipse with two rounded ends and no points. It has brilliant faceting: many small triangular and kite-shaped facets that sparkle.
- Orientation: north-south: the stone's long axis runs along the finger, at a right angle to the band. In this view the stone's length points toward and away from the camera, not along the curve of the band.
- Setting: solitaire setting: one centre stone, no halo, no side stones on the band.
- Prongs: Exactly four claw prongs, evenly spaced like the four corners of a square, none missing and none extra. Each prong is one single claw that visibly touches and grips the edge of the centre stone.
- Bridge: cathedral bridge: on each side the band itself sweeps up in one smooth, solid arch to lift and hold the head; seen from above, each shoulder widens and rises into the head as one piece, never as a second strip beside the band.
- Band: plain polished metal band: one continuous strip all the way round that does not divide near the stone, with no stones set in the band itself (the bridge stones sit on the arches only). Seen from above it is exactly one strip of metal on each side of the stone.
- Stones: this is the complete list of stones on the ring. There are no others anywhere.
  - the centre stone
  - a single row of small round rich green emerald stones set along the top edge of each cathedral arch, on both sides of the head, running from the head down to where the arch meets the band; the band itself has no stones
  - one small round pink tourmaline set in the gallery directly under the centre stone, visible from the side; it is the only stone in the gallery

Square image. One ring only. No hands, props, boxes, logos, watermark or text.

Avoid:
- adding any stone, halo, milgrain, prong or other detail that is not described above.
- drawing the centre stone with a pointed end (pear), two pointed ends (marquise), or a round outline.
- long parallel step facets (an emerald-cut look) in the centre stone.
- adding white claws beside metal-coloured ones: there is one set of claws, and all of them are white gold.
- a split shank, a twisted band, or two strips of metal side by side or a gap running along the band on either side of the stone.
- an open window or hole between the band and the head: each arch is the band itself curving up in one solid piece.
```

(About 560 words, against 1,148 today. Fill the top view the same way from Part 1b.)

## Addendum v1.1 (2026-11-10, after Freddie's reply): prong wording

Facts from Freddie: in run 20 the two-tone pear (5-prong) got a 6th claw at the rounded end, and
the two-tone marquise (4-prong) got 6, which is the 6-prong marquise layout. The flags are
settled: the label is an HTML badge plus email and alt text (whether to burn it into the image is
an owner question), and `{STONE_ORIGIN}` becomes a test variable, not a default.

1. **Use one word, "prongs", everywhere.** The two-tone line and its check say "claws" while the
   layout says "prongs". Gemini may read "white gold claws" as extra parts. In Part 1a, 1b and
   Part 3, replace "claws" with "prongs" in the two-tone Metal line, its avoid line and the
   `extra-twoToneClaws` check (the check's id can stay).
2. **Say where the prongs aren't, as well as where they are.** That targets the exact spot where
   Gemini added prongs:
   - Pear, 5-prong: "exactly 5 prongs: one V-shaped prong covering the pointed tip, and two
     single prongs along each long side, evenly spaced. The rounded end has no prong: it is held
     by the two side prongs nearest it. No other prongs anywhere."
   - Marquise, 4-prong: "exactly 4 prongs: one at each pointed end, and only one on each long
     side, at its widest point. The long sides have no other prongs."
   - Marquise, 6-prong and pear, 4-prong: keep as they are. Run 20 gives no evidence against
     them.
3. **Optional test variant B for two-tone:** put the count back in the Metal line once, as
   "...the prongs holding the centre stone, all {PRONG_COUNT} of them, are bright white gold...".
   That repeats the count, so test it against the v1 wording on the same two rings and keep the
   one that passes.
4. **Checks:** keep the `basket` positions as they are (the V counts as one of the 5). Add the
   bare-spot sentence to the matching check, e.g. pear 5: "...and is the rounded end free of
   any prong?"; marquise 4: "...and does each long side have only one prong?"

## Addendum v1.2 (2026-11-10, after run 21, owner verdict pending): ideas, not tested

Run 21 as reported by Freddie (not owner-confirmed, so not logged): basic rings passed 2 of 2;
bridge stones option A failed 0 of 3 (stones down the shoulders, 6 of 6 over two prompts);
two-tone marquise 4-prong got 6 prongs (3 of 3); two-tone pear went 1 of 1 per variant, with
unrelated fails.

1. **WITHDRAWN in v1.3 (the owner wants one-shot renders).** Two-step edit for these two
   extras.
   Render the ring without the extra first, using the proven path that passes. Then edit that
   approved picture with "change only X". Freddie's notes say a picture plus "change only X"
   holds a design far better than words, and that "add a stone" edits held.
   - Two-tone: "Change only the colour of the prongs holding the centre stone to bright white
     gold. Keep every prong exactly where it is; add none and remove none. Change nothing else."
   - Bridge stones (A): "Add a single row of small round {ACCENT_STONE} stones along [ARCH
     PLACEMENT] only. The band and shoulders stay exactly as they are, plain polished metal.
     Change nothing else."
   - Cost: one extra image call per view, inside or over the $1 cap. That needs the owner's
     approval.
2. **Bridge stones: say where on the arch, in profile terms.** "Along the top of each arch" looks
   the same as the shoulders from most angles. If the product means stones on the side face of
   the bridge (seen in profile under the head), say: "set into the outer side face of each
   cathedral arch, visible from the side; seen from above, the band and shoulders show only
   plain polished metal." Then the top-view check expects no stones from above. This is a
   product question for the owner and CAD, not just a wording choice.
3. **Two-tone as a white-gold head.** Real two-tone rings usually have a white-gold head
   (basket and prongs) on a coloured band. Saying "the head, meaning the basket and its
   {PRONG_COUNT} prongs, is white gold" may fit Gemini's defaults better than prongs alone.
   Owner and CAD must confirm that's the product.
4. **Sample size:** one try per variant can't separate pear variant A from B, and the grey
   background and east-west turn don't look like prong effects. Re-run before choosing.

## Addendum v1.3 (2026-11-10): the bridge is the rail under the head

Owner's direction (relayed by Freddie): the bridge is the curved metal rail directly under the
centre stone that joins the prongs, seen from the side (marked in red on
`nore-freddie/drafts/owner-bridge-marked.png`). It is not the cathedral arches or the shoulders.
The owner also wants the fewest renders possible: one-shot Gemini calls, so **idea 1 in v1.2
(the two-step edit) is WITHDRAWN.** Option B (shoulders) is dropped, and option A is redefined
below.

### Corrected `{BRIDGE_STONES_LINE}` (for the Stones list)

```text
a single row of small round {ACCENT_STONE} stones set into the bridge: the narrow curved metal rail directly under the centre stone that joins the prongs together just below the stone's edge (girdle). There is a bridge on each of the two side profiles of the head (the sides you see when you look at the ring from the side, with the band running left and right), and each one holds its row of stones, facing outward, visible from the side. Only the bridge has these stones: the shoulders, cathedral arches and band stay exactly as described above.
```

### Prompt changes that go with it

1. **Never use "bridge" for the cathedral choice in the prompt.** Today's line `Bridge: cathedral
   bridge: ...` uses the same word for the arches, which is exactly what sent Gemini to the
   shoulders. Change it to `Shoulders: cathedral: on each side the band itself sweeps up in one
   smooth, solid arch...`. The customer-facing label can stay; only the prompt wording changes.
   Freddie, please also check the catalogue/UI: if the builder's "Bridge" choice means the shank
   style, that's a naming clash for the owner to settle.
2. **Band line with bridge stones:** "...with no stones set in the band itself or on the
   shoulders (the only small stones are in the bridge under the head)."
3. **Avoid line [IF BRIDGE STONES]:** "- stones on the shoulders, cathedral arches or band: the
   small stones sit only in the bridge rail under the centre stone."
4. **Top view:** add to the bridge-stones item "...from this angle the centre stone mostly
   covers the bridge; do not move the stones onto the shoulders to make them visible."
5. **The Cathedral-only gate came from the old meaning.** An under-head rail exists on most
   prong heads, so whether the extra stays Cathedral-only is now an owner question.

### Clash with the birthstone (owner decision needed)

Today's birthstone line puts it "in the gallery directly under the centre stone, visible from
the side; the only stone in the gallery". That is the same place as the bridge stones, so a ring
with both extras (like design 10) contradicts itself. Options for the owner:
- (a) The birthstone sits at the centre of the bridge row on the side facing the camera, and the
  bridge stones flank it. The birthstone line becomes "one small round {BIRTHSTONE} at the centre
  of the bridge row on one side, the same size as the bridge stones".
- (b) The birthstone moves elsewhere (e.g. set inside the band, or on the far profile).
  Placement is for the owner and CAD.
Until then, **drop "it is the only stone in the gallery"** whenever bridge stones are also chosen.

### Check questions

- `extra-bridgeStones` (3/4 view): "Look at the side of the head under the centre stone. Is
  there a row of small {ACCENT_STONE} stones set into the curved metal rail (bridge) directly
  under the centre stone, between the prongs, while the shoulders, cathedral arches and band
  have no small stones? A bridge hidden by the camera angle does not count against it."
- `band` with bridge stones: "...Is the band one plain polished strip with no stones in it or on
  the shoulders? Small stones in the rail directly under the centre stone are requested and do
  not count."
- `nothing-extra`: the stone list already names the bridge stones, so no change.
- Top view: **remove** `extra-bridgeStones`. The bridge is mostly hidden from above; just make
  sure `band` and `nothing-extra` fail any stones on the shoulders.

## How to test it (suggested; spend needs the owner's approval)

- Re-run the 3 bridge-stone rings and the two-tone pear and marquise with v1 (option A, and
  option B if the owner wants to compare). Also re-run 2 of this morning's 4 basic rings to make
  sure v1 didn't break what passed. Same rings, same caps.
- Compare first-try pass rates with today's prompt, and log the result. If you tell me the
  outcome, I'll record it as a WIN or FLOP when the owner confirms it.
