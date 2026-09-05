---
name: trip-planner
description: Trip planner for a traveler or a group. Onboards a trip (destination, where they stay, dates, who's going, pace), finds restaurants backed by Google reviews with price level and menu links, finds must-see sights with entry prices, hours, and ticket links, builds a day-by-day itinerary around where they stay, and posts a daily brief during the trip. Trigger even on implicit asks - "we're going to Lisbon in May", "we're staying at the Hoxton in Shoreditch", "where should we eat tonight", "what's a must-see near our hotel", "plan our 3 days", "how much is the Alhambra", "is the museum open Monday", "what's the plan for today".
---

## Tools & credentials

**Web search is your default tool.** It answers what to see, ticket prices, menus, opening hours,
a single restaurant lookup, and weather. Reach for Apify only with a reason (ground rule 6):

- **Google Maps** (`compass/crawler-google-places`): a ranked, filtered shortlist of many places
  at once, with rating, review count, price level, hours, website and menu fields.
- **Google Maps Reviews** (`compass/google-maps-reviews-scraper`): what reviewers actually say
  about one finalist, at volume.
- **TripAdvisor** (`maxcopell/tripadvisor`): a destination-wide top-attractions ranking when web
  results are listicle noise.

Credentials are injected by the OneCLI proxy at request time; you never handle keys. If an Apify
call returns 401/403 or "not connected," read `references/credentials.md`, then carry on with the
web-search answer meanwhile.

## The capabilities → references

Identify which capability the request maps to, then read the matching reference for the steps and
output. The body here is the routing; the references are the mechanics. The traveler's actual ask
always wins over a reference's fixed path.

| Capability | What it's for | Reference |
|------------|---------------|-----------|
| **trip-onboarding** | a new trip: destination, where they stay, dates, who's going, budget, pace; plus the traveler profile (likes, dislikes, diet) the first time | `references/trip-onboarding.md` |
| **find-food** | restaurants, cafés, bars near a point, filtered by taste and diet, with price level and menu link | `references/find-food.md` |
| **find-sights** | must-see attractions with entry price, hours on the visit day, time needed, ticket link | `references/find-sights.md` |
| **build-itinerary** | the day-by-day plan across the trip's dates, clustered by neighborhood | `references/build-itinerary.md` |
| **daily-brief** | today's plan during the trip, hours and weather re-checked; fires as a scheduled task, also on ask | `references/daily-brief.md` |

## Scheduled runs

**Turning one on:** confirm the cadence, then **list the current tasks before creating anything**;
the daily brief ships paused, so if it already exists, update its schedule and resume it rather
than adding a duplicate. Create a new task only when none exists, with the prompt "Follow the
`trip-planner` skill's `daily-brief` reference and post to this chat." Act only on a clear yes.

**Turning one off:** when the trip is over, offer to pause the brief rather than leave it firing
on empty; don't delete without asking.

## Output style

- **Phone-readable.** Bullets over paragraphs. One line per place:
  `<name> · ★<rating> (<n> reviews) · <price level or entry price> · <walk/transit from stay> · <link>`
- **Lead with the pick**, then the alternatives. Say why in a few words ("quiet, locals, great
  grilled fish").
- **Always the link**: Maps URL or official site; menu link for food; ticket link for paid entry.
- **Chunk long output** to platform limits (Telegram ~4k chars, Discord ~2k).
