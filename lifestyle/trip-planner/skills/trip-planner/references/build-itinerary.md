# Build Itinerary

The day-by-day plan across the trip's dates: morning, afternoon, evening per day, clustered by
neighborhood, at the traveler's pace, with a meal from the food shortlist at each mealtime.

**A plan is a proposal.** Show it, ask for one reaction, revise. Never book anything from it
without a clear yes.

## Steps

1. **Ground.** Read the profile (pace, rhythm, walking tolerance, kids) and the trip (dates, stay,
   the food and sights shortlists). If a shortlist is missing, run `find-sights` and `find-food`
   first (web search; escalate to Apify only per their rules).

2. **Verify the calendar with code**: every date's weekday, the arrival and departure days (half
   days), and local public holidays for the range (one web search).

3. **Check closed days.** For each shortlisted sight, match its closed days and hours against the
   trip dates; a place closed Monday goes on another day. Timed-entry places get a "book by" note.

4. **Cluster by neighborhood.** Group sights that are near each other into the same day; put the
   day's meals in the same area. Start each day close to the stay when the rhythm is slow, far when
   it's early-riser.

5. **Pace.** Packed: 3 to 4 stops a day. Slow: 2, with a long lunch. Kids or mobility limits: 2,
   with a rest in the middle. Arrival day: one easy stop near the stay. Leave one evening open.

6. **Budget.** Sum the entry fees per day from the sights shortlist and show the total; flag when a
   day runs hot for the stated tier.

7. **Save** to the trip concept. After the reaction, update the plan and the profile.

## Output

```
📅 <destination>, <first date> – <last date>, staying at <stay>

Day 1 · <weekday> <date> (arrival)
- Afternoon: <sight> · <price or free> · <hours> · tickets: <link>
- Dinner: <restaurant> · <price level> · menu: <link> · <walk from stay>

Day 2 · <weekday> <date> · <neighborhood>
- Morning: <sight> · <price> · <hours> · ~<time needed> · tickets: <link> · book ahead
- Lunch: <restaurant> · <price level> · menu: <link>
- Afternoon: <sight> · ...
- Evening: <sight or "open">

...

Entry fees: ~<total + currency> for <n> people. <closed-day notes, timed-entry deadlines>
```

Chunk to platform limits; one day per message on Discord if needed.
