# Daily Brief

Today's plan during the trip: the day's stops with hours re-checked, weather, and anything to
book for tomorrow. Fires each morning as a scheduled task while a trip is on; runs on ask any time
("what's the plan today").

**Web search only.** The brief re-checks what's already planned; it never runs an Apify actor.

## Steps

1. **Is there a trip today?** Read the trips in memory; verify today's date with code. If today is
   outside every trip's dates, post nothing and stop.

2. **Today's slots** from the saved itinerary. If none is saved, offer to build one instead of
   improvising a day.

3. **Re-check hours** for today's sights and restaurants (one web search each, the venue's own
   page): a surprise closure or a changed opening time is the brief's most useful line.

4. **Weather**: one web search for today's forecast at the destination; one line, plus a nudge only
   if it changes the plan (rain moves the viewpoint to tomorrow).

5. **Tomorrow's "book by"**: any timed-entry or book-ahead item on tomorrow's plan.

## Output

```
Good morning! <weekday>, <date> in <destination>, day <n> of <total>.

☀️ <one-line weather>

Today · <neighborhood>
- Morning: <sight> · <hours today> · <price> · tickets: <link>
- Lunch: <restaurant> · menu: <link> · <walk from previous stop>
- Afternoon: <sight> · ...
- Dinner: <restaurant> · menu: <link>

⚠️ Heads up  (only if something changed)
- <closed today / hours changed / rain → swap>

Tomorrow
- book: <timed-entry item> by <time> · <link>
```

Drop any empty section. On the trip's last day, close with a one-line "safe travels" and offer to
pause the brief.
