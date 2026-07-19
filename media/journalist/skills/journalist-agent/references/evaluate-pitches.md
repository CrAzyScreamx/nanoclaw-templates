# Evaluate Pitches

Score inbound pitches against the beat so the journalist reads only what
matters. Pitches arrive however they arrive: pasted into chat, forwarded as
a batch, or sitting in an inbox if a mail tool is connected. Check what
sources you actually have available, use what is there, and tell the user
which source you worked from.

## The pitch ledger

`/workspace/agent/pitch-ledger.md` tracks every pitch ever seen, one line
each: a stable id (message id, URL, or date + sender), subject or first
line, date seen, status (`new` / `evaluated`), and verdict. The ledger is
what keeps you from re-reading the same 300 emails three times a day, and
it works the same for any source of pitches.

## Steps

1. **Inventory first, content later.** List what arrived: ids and subjects
   only, no bodies yet. Append everything not already in the ledger as
   `new`, and skip everything already there. For a large backlog this pass
   is cheap and gives the user an immediate count.

2. **Evaluate incrementally.** Work through `new` items one by one (batches
   of 10–20 for big backlogs), reading each pitch's full text only when its
   turn comes. Mark each `evaluated` with its verdict in the ledger as you
   finish it, so progress survives even if the session stops mid-batch.

3. **Score each pitch on its text alone**:
   - Beat fit: on-beat and on-angle / adjacent / off-beat
   - Newsworthiness: new, timely, consequential vs. a warmed-over
     announcement
   - Exclusivity: offered first / embargo / already everywhere
   - Specificity: real names, data, and access offered vs. vague claims

4. **Verify the sender** (only for survivors): one Exa lookup. Does the
   person/company exist, do the claims hold at a glance, any red flags?
   When the pitch links out to stories or data that bear on the verdict,
   fetch those pages too (Exa can pull a URL's contents). If a link cannot
   be fetched, judge the pitch on its text and say so in the verdict table
   ("link unreachable, judged on text alone") so a good pitch is never
   quietly downgraded over a broken fetch.

5. **Report a verdict table**, one row per pitch: pursue / maybe / pass,
   with a one-line rationale. For each **pursue**, add the suggested next
   step (a question back to the pitcher, or straight to
   `references/find-sources.md`).

6. **Learn**: when the user overrules a verdict, update the beat profile's
   angles or not-interested list so the same call goes right next time.

7. **Close the loop on the source**: if the pitches were pasted or
   forwarded, suggest connecting the mailbox they come from so the next
   pass runs hands-off. Once a mailbox is connected, offer to keep an eye
   on it and surface important mail regularly, not only pitches. If they
   accept, propose it as a scheduled task (cadence of their choice, e.g.
   hourly) and, once they approve, create the task.
