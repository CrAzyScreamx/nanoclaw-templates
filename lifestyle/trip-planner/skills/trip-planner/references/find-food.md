# Find Food

Restaurants, cafés, and bars near a point, filtered by the traveler's tastes and diet, with the
price level and a menu link. The point defaults to where they stay; a named landmark or
neighborhood overrides it ("lunch near the Alhambra").

**Web search first.** A single "where do we eat tonight" is usually answered entirely by web
search. Apify enters only for a shortlist across a neighborhood or a review-backed ranking, and
you say so in one line.

## Steps

1. **Ground.** Read the traveler profile (diet, dislikes, budget, cuisines) and the trip (stay
   location, who's going, the day and meal in question). Verify the weekday with code.

2. **Web search** for candidates: "best <cuisine> <neighborhood>", local food blogs and papers,
   the venues' own sites. Collect name, cuisine, rough price level, address, and the menu page.
   Drop anything that hits a dislike or dietary rule. For a single pick, stop here and go to
   step 5.

3. **Shortlist sweep (Apify, only when asked for a shortlist or a ranked list).** Run
   `compass/crawler-google-places` **once** with:
   - `searchStringsArray`: one or two broad strings from profile + ask ("seafood restaurant",
     "vegetarian restaurant")
   - `locationQuery`: the stay address, or "<landmark>, <city>"
   - `maxCrawledPlacesPerSearch`: 20, `maxReviews`: 0, `maxImages`: 0
   - `language`: the traveler's
   Filter: rating ≥ 4.3 and `reviewsCount` ≥ 100 (relax both when the area is thin), drop
   dislikes, check `openingHours` against the target day. Rank by rating × log(reviews), then
   proximity. Keep the top 5 to 8. Push the sweep to a subagent when it's part of a bigger plan.

4. **Review digest (Apify, only for the finalists and only when they ask what people say).** For
   at most 3 to 5 places run `compass/google-maps-reviews-scraper` with `maxReviews` 30, newest
   first. Distill to one line each: what reviewers praise, what they complain about, any "book
   ahead" or "cash only" warnings.

5. **Menu and price link.** Web search "<name> menu" and prefer the venue's own menu page; the
   actor's `menu` field, then `website`, are fallbacks. Note the price level (`$`–`$$$$` or the
   actor's `price`) and, when a menu shows it, a typical main's price with currency.

6. **Distance.** A rough walk or transit time from the stay location (one web search or the
   actor's coordinates). Nudge-level, not an ETA.

7. **Save** the shortlist to the trip concept with the source of each entry. After they pick or
   react, update the profile (a new liked cuisine, a dislike confirmed).

## Output

```
🍽️ <meal>, <weekday> <date>, near <stay / landmark>

Pick
- <name> · ★<rating> (<n>) · <price level> · <cuisine> · <walk/transit> · menu: <link> · <maps link>
  <one-line why, and any warning: book ahead / cash only / closes 15:00>

Also good
- <name> · ★<rating> (<n>) · <price level> · <cuisine> · <walk/transit> · menu: <link> · <maps link>
- ...

<one line: "from web search" or "shortlist via Google Maps (20 places), reviews for the top 3">
```

Drop the rating and count when a place came from web search alone and you couldn't confirm them;
never invent a number.
