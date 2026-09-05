# Find Sights

Must-see attractions for the destination or a part of it, each with entry price, hours on the
visit day, time needed, distance from the stay, and the ticket link.

**Web search first.** The destination's must-sees and each venue's official site (price, hours,
tickets) are on the open web; that covers most trips. TripAdvisor via Apify enters only when web
results are listicle noise or the traveler wants a ranked list with review counts, and you say so.

## Steps

1. **Ground.** Read the profile (sights taste, crowd tolerance, kids, mobility) and the trip (stay
   location, dates). Verify the weekdays with code.

2. **Web search** for the destination's must-sees: official tourism site, a couple of reputable
   guides, and "<destination> things to do <month>" for seasonal ones. Build a candidate list of
   10 to 15. Drop what the profile says to skip ("seen it," "no museums").

3. **Per candidate, the venue's own page**: entry price with currency and any free/reduced
   categories, ticket or booking URL, opening hours (and closed days), typical visit length,
   "book ahead" or timed-entry notes. Record the page and the date you read it. If the official
   site doesn't state a price, say "check on site"; don't take a blog's number.

4. **Ranked list (Apify, only when needed).** Run `maxcopell/tripadvisor` once for the
   destination's attractions, `maxItems` 20, and cross-check the top entries with one
   `compass/crawler-google-places` run (`searchStringsArray` such as "tourist attraction",
   "museum"; `maxCrawledPlacesPerSearch` 20, `maxReviews` 0). Use their rating and review count to
   order the list; keep the official site as the source for price and hours.

5. **Distance and clustering.** A rough walk or transit time from the stay; note the neighborhood
   so `build-itinerary` can group them.

6. **Save** the shortlist to the trip concept with sources. After a reaction, update the profile.

## Output

```
🗺️ Must-sees for <destination>, staying near <stay>

- <name> · ★<rating> (<n>) · <price + currency, or "free"> · <hours on visit day> · ~<time needed> · <walk/transit> · tickets: <link>
  <one-line why; "book ahead" / "timed entry" / "closed <day>" if it applies>
- ...

Prices from each venue's site as of <date>. <"from web search" or "ranked via TripAdvisor (20) + Google Maps">
```

Drop the rating and count when unconfirmed; never invent a number or a price.
