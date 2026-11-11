# Bypass ring, oval: Gemini prompts (3/4 view and top view)

- From: Peter, 2026-11-10. For: Freddie. Status: PROPOSAL, not rendered. The owner approves any
  render spend.
- Ring: Hers, 14k white gold, lab-grown colourless diamond, oval about 1.50 ct, north-south,
  solitaire, 4 claw prongs, Low/Flat, Bypass band. No extra stones, no milgrain.
- Engine: gemini-3-pro-image, one square image per call. The top view gets the approved 3/4 image
  as its reference.
- Sources I read: your run 25 prompt (`bypass-prompt-run25-front.txt`), the builder's bypass
  tile, and the gallery-test images `nb-bypass-white-oval-front-1`, `-v2-front-1` and
  `-v2-top-1`. I'm assuming those are runs 24 and 25; tell me if they aren't.

## What I changed, and why

1. **The style line said "symmetrical band".** Your base line asks for "a clean, symmetrical,
   physically sound band", and the band line then asks for a band that is not symmetrical. That
   is the likeliest cause of run 24's plain solitaire. The word is removed here. For the
   template: drop "symmetrical" from the base line whenever the band is Bypass.
2. **The bypass is now tied to the prongs.** "Curve past each other, one in front and one
   behind" doesn't say where the ends go. Here each end flows into a named place: the prong at
   one rounded end of the oval, and the prong at the other rounded end. That is what the passed
   top view shows.
   **v2 (owner's answer, 2026-11-10): the four prongs sit at the tips and sides**, one at each
   rounded end and one at the middle of each long side, not at the corners. The Prongs and Band
   lines in both prompts were changed together to match.
3. **The stone's direction is tied to the opening of the ring, not to the band.** "At a right
   angle to the band" has no clear meaning once the band swerves. In run 25's 3/4 view the oval
   lay along the band and faced the camera. The new wording uses the ring's opening (the way a
   finger goes through), says which ends of the oval are near and far, and says the band's ends
   reach the long sides.
4. **The table is described as it should look from this camera:** level, seen at a slant, with
   the side of the stone visible. "Never turned to face the camera" alone didn't hold.
5. **Each fact once.** About 480 words per view, against 944.
6. **One word for the prongs** ("prongs" everywhere; "claw" only describes the tips).
7. **"Bridge" is not used.** The owner's "bridge" is the gallery rail, so Low/Flat is written as
   "Height: low-set".
8. **"lab-grown" is in the stone line**, because NORE's prompt rule requires it. It is the one
   word your runs haven't tested. It should not change the picture.

Catalogue lines kept word for word: metal, setting. Reworded: basket, bridge, band, stone
seating, orientation. Your pre-render check will need to allow that for this test.

---

## Prompt 1: 3/4 view

```text
Macro commercial jewellery studio photograph of one fine-jewellery ring: photorealistic, seamless pure white background, soft softbox lighting with realistic metal reflections and diamond brilliance, razor-sharp focus, 100mm macro lens. Accuracy matters more than artistic flair: render exactly the ring described below, with crisp individual prongs, realistic faceting and a clean, physically sound band.

Camera: 3/4 view. The ring stands upright on the bottom of its band, turned about 30 to 45 degrees so the camera sees partly through the opening of the ring, with the camera slightly above. The centre stone is at the very top of the ring. Its flat top (table) is level and faces straight up at the ceiling, so from this camera the table is seen at a slant, with the side of the stone and its prongs visible below it. The stone is never tilted to face the camera.

The ring (each part is described once; render exactly this):
- Ring for: women's ring.
- Metal: 14 karat white gold (bright silvery white), for the whole ring.
- Centre stone: one lab-grown colourless white diamond, oval cut, about 1.50 carat, in realistic proportion to the band. The outline is an elongated ellipse with two rounded ends and no points. It has brilliant faceting: many small triangular and kite-shaped facets that sparkle.
- Orientation: north-south. The long axis of the oval points the same way as the opening of the ring, the direction a finger passes through it. In this view one rounded end of the oval is nearer the camera and the other is farther away, and the oval's two long sides face the left and right sides of the band. The oval never lies lengthwise along the curve of the band.
- Setting: solitaire setting: one centre stone only, no side or halo stones.
- Prongs: exactly four prongs with claw tips: one at each rounded end of the oval, and one at the middle of each long side. There are no prongs at the corners in between. Each is one single prong that visibly touches and grips the edge of the stone.
- Height: low-set. The head sits down into the band, so the bottom tip of the stone (culet) rests at the top of the band, with no air gap, post or pedestal under it.
- Band: bypass band. The band is one smooth, polished, rounded strip of metal whose two ends do not meet the head directly opposite each other. The end coming up the left side of the ring swerves toward one rounded end of the oval and flows into the base of the prong at that end. The end coming up the right side swerves the opposite way and flows into the base of the prong at the other rounded end. Each end narrows gently as it sweeps in. Seen from above, the two ends and the stone make a soft S shape with the stone held in the middle of the S. The two ends never touch each other, never cross over the stone, and neither one divides in two.

Square image. One ring only. No hands, props, boxes, logos, watermark or text.

Avoid:
- a band whose two sides rise evenly and meet the head directly opposite each other, like a classic symmetrical solitaire: the two ends are clearly offset, one toward each end of the oval.
- turning the oval so its long axis follows the band, or tilting its face toward the camera.
- an open gap, arches or a tall basket under the stone.
- either end of the band splitting into two strands, or a twisted rope band.
- any halo, hidden halo, side stones, small stones, milgrain, engraving or other detail not described above.
- a pear, marquise or round outline, or long parallel step facets, in the centre stone.
```

## Prompt 2: elevated top view (approved 3/4 image attached)

```text
Macro commercial jewellery studio photograph of one fine-jewellery ring: photorealistic, seamless pure white background, soft softbox lighting with realistic metal reflections and diamond brilliance, razor-sharp focus, 100mm macro lens. Accuracy matters more than artistic flair: render exactly the ring described below, with crisp individual prongs, realistic faceting and a clean, physically sound band.

Camera: elevated top view. The ring stands upright; the camera is above and in front of it, about 35 to 45 degrees from straight down, looking onto the face of the centre stone. The stone sits in the lower part of the picture; the opening of the ring and the far side of the band are seen above and behind it. The shot is not flat from straight above and not from a low side angle.

Reference: the attached image is the approved 3/4 view of this exact ring. Show the same ring (same stone, shape, colour, setting, prongs, band and metal) from this new camera angle, and keep each end of the band on the same end of the stone as in the reference. Change only the camera. Some prongs are hidden behind the stone in the reference: draw every prong described under Prongs, not only the ones visible there.

The ring (each part is described once; render exactly this):
- Ring for: women's ring.
- Metal: 14 karat white gold (bright silvery white), for the whole ring.
- Centre stone: one lab-grown colourless white diamond, oval cut, about 1.50 carat, in realistic proportion to the band. The outline is an elongated ellipse with two rounded ends and no points. It has brilliant faceting: many small triangular and kite-shaped facets that sparkle.
- Orientation: north-south. The long axis of the oval points the same way as the opening of the ring, the direction a finger passes through it. In this view the oval's long axis runs up and down the picture, toward and away from the camera, and the two ends of the band come in from the left and the right. The oval never lies lengthwise along the band.
- Setting: solitaire setting: one centre stone only, no side or halo stones.
- Prongs: exactly four prongs with claw tips: one at each rounded end of the oval, and one at the middle of each long side. There are no prongs at the corners in between. Each is one single prong that visibly touches and grips the edge of the stone.
- Height: low-set. The head sits down into the band, with no air gap, post or pedestal under the stone.
- Band: bypass band. The band is one smooth, polished, rounded strip of metal whose two ends do not meet the head directly opposite each other. The end coming in from the left swerves toward one rounded end of the oval and flows into the base of the prong at that end. The end coming in from the right swerves the opposite way and flows into the base of the prong at the other rounded end. Each end narrows gently as it sweeps in. From this angle the two ends and the stone make a soft S shape with the stone held in the middle of the S. The two ends never touch each other, never cross over the stone, and neither one divides in two.

Square image. One ring only. No hands, props, boxes, logos, watermark or text.

Avoid:
- a band whose two sides meet the head directly opposite each other, like a classic symmetrical solitaire: the two ends are clearly offset, one toward each end of the oval.
- turning the oval so its long axis follows the band.
- either end of the band splitting into two strands, or a twisted rope band.
- any halo, hidden halo, side stones, small stones, milgrain, engraving or other detail not described above.
- a pear, marquise or round outline, or long parallel step facets, in the centre stone.
- large bright white glare patches on the band; keep metal reflections soft and even.
```

---

## Run 26 result (2026-11-11): v2 FAILED by check and by eye; owner's verdict pending

As reported by Freddie, and I've looked at `peter-bypass.jpg`: both views are a plain symmetrical
solitaire with cathedral-style shoulders and a gap under the stone. No bypass. The prongs are
nearer the corners than the tips and sides. The oval is north-south and its table is level,
but that is the easy case on a symmetrical ring, so it proves little.

**Do not render v2 again.** What I got wrong:

1. I rewrote the one sentence that had worked. Run 25's "one end passing in front of the stone
   and the other behind it, so the band is clearly not symmetrical from any angle" produced a
   bypass in the 3/4 view once and in both top views. My replacement ("comes up the side,
   swerves, flows into the base of the prong, narrows gently, soft S") reads like a description
   of cathedral shoulders rising into a head, and that is what Gemini drew.
2. I cut the repetition. Run 25 says the band is not symmetrical three times (Band, Band form,
   DON'T). "Say each fact once" helped on the standard rings, but a feature that fights
   Gemini's default seems to need the weight.
3. My "symmetrical in the style line" diagnosis was not the main cause: run 25 had that word
   and still drew a bypass.

### v3, option 1 (words only): run 25's prompt with three lines changed

Start from `bypass-prompt-run25-front.txt` exactly as it is, since the owner passed it. Change
only these lines, so the test has one variable (the stone's direction):

- **Band** (keep your sentence, add the last two): "bypass band: the two ends of the band curve
  past each other around the centre stone instead of meeting it head-on, one end passing in
  front of the stone and the other behind it, so the band is clearly not symmetrical from any
  angle. 'In front' means beside the rounded end of the oval nearest the camera, and 'behind'
  means beside its far rounded end. Only the band swerves; the stone does not turn to follow
  it."
- **Stone orientation** (replace): "north-south: the long axis of the oval points the same way
  as the opening of the ring, the direction a finger passes through it. In this view one
  rounded end of the oval is nearer the camera and the other is farther away. The oval never
  lies lengthwise along the curve of the band."
- **Stone seating** (replace the last sentence): "...Its flat top is level and faces straight up
  at the ceiling, so from this camera it is seen at a slant, with the side of the stone and its
  prongs visible below it. It is never tilted to face the camera."
- **Prong layout**: your tips-and-sides line for Bypass ovals, as now in the code.

Honest odds: this keeps what produced the bypass and only tightens the direction of the stone.
Run 25 already failed on that direction once, so this is not a sure first-time pass.

### v3, option 2 (reference picture): I think this is the stronger route

Your own notes say an approved picture plus "change only X" holds a design far better than
words, and Gemini's pull toward a classic solitaire is exactly a words problem. It also fits the
owner's rule: still one call per view, with one reference image, and no extra render.

- Reference for the 3/4 call: the owner-passed bypass top view (`nb-bypass-white-oval-v2-top-1`)
  or, better, an owner-approved 3/4 bypass picture once one exists.
- Reference line (third in the prompt, after the camera line): "The attached image is an approved
  NORE ring with a bypass band. Copy its band exactly: the way the two ends of the band sweep
  past the centre stone on opposite sides instead of meeting it head-on. The camera angle, metal,
  stone, shape and prongs come from the description below, not from the image."
- Then the ring description and avoid list as in option 1.
- Risk to check on the first render: Gemini may also copy the reference's camera angle. The
  camera line stays second, and the check should fail a top-view angle on the 3/4 call.

## Check questions to match (suggested)

- `band` (both views): "Do the two ends of the band reach the head at different ends of the
  centre stone, offset from each other (a bypass), and not directly opposite each other as on a
  symmetrical solitaire? Is neither end split into two strands?"
- `orientation` (3/4 view; add it if this view has none): "Does the oval's long axis point
  through the opening of the ring, with one rounded end nearer the camera and one farther, and
  not along the curve of the band?"
- `seating` (3/4 view): "Is the stone's flat top level and facing up, seen at a slant from this
  camera, and not tilted to face the camera?"
- `basket` (owner's answer: tips and sides): "Count the prongs holding the centre stone. Are
  there exactly 4 single prongs: one at each rounded end of the oval and one at the middle of
  each long side, with none at the corners in between?" Your current check says "four corners of
  a square", which would fail this layout.

## Things to know before the render

1. **Prong positions are the owner's choice: tips and sides** (answered 2026-11-10). The
   catalogue's 4-prong oval line says "like the four corners of a square". Whether that line
   should change for every 4-prong oval, or only for the bypass band, is a question for the
   owner.
2. **Which end goes which way is left open in the 3/4 view** on purpose; the top view follows
   the reference. If NORE's bypass always sweeps one way, tell me and I'll fix the direction.
3. **A north-south oval in a bypass is unusual.** Most bypass rings in photos hold the stone
   diagonally or sideways, which is the pull behind run 25. If the 3/4 view still turns the
   stone, the next thing to try is wording, not a second render of the same prompt.
4. **Not tested.** Please send me the owner's verdict on the pair so I can log it.
