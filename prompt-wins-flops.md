# Prompt Wins & Flops — NORE Jewellery

The "Prompt Wins & Flops" memory. Read at the start of every chat. Logged on "WIN:" or "FLOP:".
Append at the bottom with the next entry number. Results are the owner's facts only.

Entry format:

```
## Entry #N — WIN | FLOP
- Date: YYYY-MM-DD
- Prompt (library # if saved) and tool / agent:
- Result (owner's facts only):
- Why it worked or failed:
- Lesson:
- New rule: (if any, also saved in prompt-rules.md as Entry #N)
```

---


## Entry #1 — WIN
- Date: 2026-11-10
- Status: CORRECTED by #3 (the owner later failed ring 2's top view, so only ring 3 is a
  confirmed pass; ring 2's 3/4 view still passed)
- Prompt (library # if saved) and tool / agent: Ring builder render template v1.3, bridge-stones
  line ("bridge" = the curved rail under the head, and the word "bridge" removed from the
  cathedral line); Gemini gemini-3-pro-image, via Freddie's builder code. Draft:
  drafts/ring-builder-normal-template-v1.md. Not in the library.
- Result (owner's facts only, relayed by Freddie, owner-confirmed): run 22. The owner passed 2 of
  3 rings (rose with sapphire bridge stones; rose with all four extras): the stones sat on the
  curved bar under the head, where the owner circled. Runs 20–21 with the old wording put the
  stones down the shoulders 6 of 6 times.
- Why it worked: the prompt defined the part by where it sits and what it looks like, and
  stopped using the same word ("bridge") for two different parts (the cathedral arches).
- Lesson: for Gemini, define every part by its position and look, not just its name, and never
  give two parts the same name in one prompt.
- New rule: none (the owner hasn't given one).

## Entry #2 — FLOP
- Date: 2026-11-10
- Prompt (library # if saved) and tool / agent: same v1.3 bridge-stones line, the phrase "joins
  the prongs together just below the stone's edge (girdle)"; Gemini gemini-3-pro-image.
- Result (owner's facts only, relayed by Freddie, owner-confirmed): run 22, ring 1 (yellow,
  bridge stones alone) FAILED. Owner: "as its on the halo not the bridge"; the stones hugged the
  underside of the centre stone.
- Why it failed: "just below the girdle" describes where a hidden halo sits; the real bridge is
  lower, below the base of the prongs.
- Lesson: place each part relative to the nearest part Gemini could confuse it with, and say
  which look it must NOT be (here: not a hidden halo). Freddie's corrected line ("lower down
  below the base of the prongs ... NOT a ring of stones hugging the underside of the centre
  stone") has only been re-checked against the 6 existing images (agrees with the owner 3 of 3),
  not rendered yet.
- New rule: none (the owner hasn't given one).

## Entry #3 — FLOP
- Date: 2026-11-10
- Prompt (library # if saved) and tool / agent: ring builder bridge-stones line, top view (v1.3
  plus Freddie's correction, which ruled out the shoulders but did not mention the halo rail);
  Gemini gemini-3-pro-image.
- Result (owner's facts only, relayed by Freddie): run 22, the rose gold ring with sapphire bridge
  stones. Its 3/4 view put the stones on the gallery rail: PASS. Its top view put them on the halo
  rail: FAIL. Owner: "#22 should be a fail as the stones are on the halo rail not the gallary
  rail". This corrects WIN #1, which counted that ring as a pass.
- Why it failed: from above, the gallery rail is hidden under the stone, so Gemini moved the
  stones up to the nearest visible place, the halo rail just under the girdle. The prompt only
  ruled out the shoulders.
- Lesson: when a part is hidden in one view, name every nearby place the stones could drift to
  and say each stays plain. For bridge stones: "the halo rail has no stones". Use the owner's
  terms: halo rail (at the edge of the stone, just under the girdle) and gallery rail (lower,
  curved, under the head = the bridge).
- New rule: none (the owner hasn't given one). Freddie's top-view wording now says: "do not move
  the stones onto the shoulders or up onto the halo rail... the halo rail has no stones".

## Entry #4 — FLOP
- Date: 2026-11-11
- Prompt (library # if saved) and tool / agent: Peter's bypass oval prompts v2, 3/4 view and top
  view (drafts/bypass-oval-prompts.md); Gemini gemini-3-pro-image, rendered word for word by
  Freddie as run 26. Not in the library.
- Result (owner's facts only, relayed by Freddie): FAIL, both views. Owner: "peters is not by
  pass thats a messed up solitare ours is a bypass". Run 25 (Freddie's template with "one end
  passing in front of the stone and the other behind it ... not symmetrical from any angle") is
  the owner's reference for what a NORE bypass looks like. Cost of run 26: $0.31.
- Why it failed: Peter rewrote the sentence that had already produced a bypass. The new wording
  (each end "swerves" and "flows into the base of the prong", "narrows gently", "soft S") reads
  like cathedral shoulders rising into a head. Peter also removed the repetition: run 25 says
  the band is not symmetrical three times.
- Lesson: (1) When an owner-passed prompt exists, start from it and change one thing at a time;
  never rewrite the wording that produced the pass. (2) "Say each fact once" suits standard
  rings, but a feature that goes against Gemini's default (here, a non-symmetrical band) needs
  its proven wording and its repetition kept. (3) A first render of rewritten wording is a
  test, not a likely pass; say so before the spend.
- New rule: none (the owner hasn't given one).
