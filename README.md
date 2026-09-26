# Mandarin Learner Tracker

This repository is the canonical progress record for Mandarin practice with ChatGPT.

## Files

- `learner.json` — stable learner preferences, goals, and high-level state.
- `vocab.json` — vocabulary knowledge, review history, and production/recognition performance.
- `grammar.json` — grammar structures, mastery state, recurring errors, and review history.
- `sessions/` — short session summaries. These are not full transcripts.

## Operating rules

1. Read the current learner state before planning a lesson.
2. Prefer production over passive recognition when practical.
3. Do not keep drilling already-solid items just because they are salient in recent chat context.
4. Reintroduce older material using spaced review.
5. Track recognition and production separately.
6. After a meaningful practice session, update the affected records and add a short session summary.
7. Keep this repo as the canonical granular record; use ChatGPT memory only for durable preferences and broad context.

## Mastery model

Vocabulary and grammar items use these states where applicable:

- `new`
- `learning`
- `shaky`
- `productive`
- `solid`

A solid item should mostly disappear from explicit drilling and return through incidental use or overdue review.
