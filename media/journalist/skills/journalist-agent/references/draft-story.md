# Draft the Story & Editor Pitch

Turn interview material and research into a draft the journalist can edit,
plus the pitch that sells it to an editor.

## Editor pitch (often wanted before the draft)

One tight block: working headline + dek, a 3-sentence pitch (what's new, why
now, why our readers), sources lined up, expected length, what's still
unconfirmed.

## Drafting steps

1. **Load**: the story folder (`/workspace/agent/stories/<slug>/`), the
   beat profile, and the writing samples in `/workspace/agent/style/`.
   Match the samples' voice; if there are no samples yet, ask for 2–3
   published pieces (see `references/onboard-journalist.md`) or use neutral
   news style and say so.

2. **Pull quotes word-for-word.** Copy each quote from the notes or
   transcript exactly as the person said it. You may drop filler ("um",
   repeated words, false starts) if you mark the quote `[cleaned]` so the
   journalist knows it is tidied. Any change beyond that makes it a
   paraphrase: present it as one, in your words, without quote marks.

3. **Structure** (default news feature; adapt to the outlet's format):
   - Lede: the most newsworthy concrete thing
   - Nut graf: why this matters, why now
   - Body: alternate evidence and voices; one idea per paragraph
   - Kicker: forward-looking or the best remaining quote

4. **Length**: hit the target from the beat profile or the request
   (typically 300–1,500 words); ask if ambiguous between a brief and a
   feature.

5. **Add a fact-check appendix after the copy**, so the journalist can
   verify the draft fast. Three parts:
   - a table mapping every factual claim in the draft to its source
   - the open `[VERIFY]` list: anything still unconfirmed
   - every quote used, with where it appears in the notes/transcript

6. **Persist** to `/workspace/agent/stories/<slug>/draft-vN.md`.

If the journalist ever shares the version they actually filed, compare it
with your draft and fold the recurring corrections into the notes in
`/workspace/agent/style/`; their real edits are the best style guide there
is.
