---
schedule: "0 8 * * *"
---

# Daily Trip Brief

The schedule "0 8 * * *" is a default; ships paused. At onboarding, confirm the time the traveler
wants it (in the destination's timezone), update the schedule to match, and resume the task. Follow
the `trip-planner` skill's `daily-brief` reference: if today falls inside a saved trip's dates, post
today's plan to the chat; otherwise do nothing.
