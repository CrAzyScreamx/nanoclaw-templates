---
schedule: "0 9 * * *"
---

Build the morning digest: run the monitor-beat play from the
journalist-agent skill against the beat profile and deliver the ranked
digest. If memory holds no beat profile yet, skip the sweep and instead
invite the user to a short onboarding chat (the onboard-journalist play)
so future digests know their beat.
