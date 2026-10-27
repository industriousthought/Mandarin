# Mandarin Learner Tracker

This repository maintains the canonical progress record for Mandarin practice with ChatGPT **and** a simple, mobile-friendly flashcard app.

## Start here

- **`docs/progress.json` — canonical, complete learner record.** It includes the learner profile, all vocabulary and grammar entries, and app review events in `review_log`. It was initially migrated from the historical files on October 27, 2026.
- `docs/index.html` — a self-contained, dependency-free flashcard app for GitHub Pages. It reads `./progress.json`, saves new review events locally, and can copy them to the clipboard.
- `learner.json`, `vocab.json`, `grammar.json` — historical, pre-migration records, retained as provenance. **Do not update these separately** or assume they are newer than `docs/progress.json`.
- `sessions/` — short, historical and ongoing lesson summaries; not complete transcripts.

## GitHub Pages setup (one-time)

1. Review the repository contents before making it public; GitHub Pages exposes both the app and the progress data, and public repositories expose every committed file.
2. In repository **Settings → General → Danger Zone**, change visibility to **Public** if desired.
3. In **Settings → Pages**, select **Deploy from a branch**, branch **main**, folder **/docs**, and save.
4. Open **https://industriousthought.github.io/Mandarin/** in Safari. You can add it to the iPhone Home Screen.

GitHub Pages is read-only. The app cannot directly commit progress to GitHub. Browser storage is device/browser-specific and may be cleared.

## Reviewing cards and syncing

1. Open the flashcard app. It fetches `docs/progress.json` and merges any locally stored reviews by unique event ID, preserving unsynced reviews.
2. Choose **Hanzi → English** (recognition) or **English → Hanzi** (production). Self-rate after revealing the answer. Cards are scheduled independently by direction; mastered material comes up less often.
3. Select **Copy progress JSON** and paste the compact `mandarin-review-update` JSON into a ChatGPT Mandarin session. **Only reviews not present in the currently loaded GitHub snapshot** are included.
4. In ChatGPT, merge review entries by their `id` into `docs/progress.json.review_log` (without dropping any existing entries); update other knowledge, weaknesses, or notes as appropriate; advance `updated_at` (ISO 8601); commit the updated record.
5. Refresh the app after the commit is published on Pages. Newly synced events cease to count as pending. Never overwrite the repo snapshot wholesale from an older browser export; merge events and learner edits.
6. For device-to-device backup, use **Copy full snapshot**, or expand the import panel and paste either a complete snapshot or a compact review-update export.

### JSON contract

- `schema_version: 1`
- `updated_at`: timestamp of last canonical edit
- `learner`, `vocab`, `grammar`: existing nested tracker schemas, preserved in full
- `review_log`: append-only array of objects with `id`, `type` (`vocab` or `grammar`), `key`, `direction` (`recognition` or `production`), `rating` (`again`, `hard`, `good`, `easy`), and `at` (ISO timestamp)
- `exported_at`: optional marker in a copied full snapshot, not a commit timestamp

The app uses a simple interval scheduler, separate per review direction. This is an initial heuristic, not a validated learning algorithm. App rating data does **not** automatically overwrite the historical recognition/production counts; when reconciling, preserve the difference between conversational evidence and self-rated flashcard recall.

## Tutoring principles

1. Read `docs/progress.json` before planning a lesson.
2. Prefer production over passive recognition when practical.
3. Avoid repetitive drilling of already-solid concepts; bring older material back when overdue.
4. Track recognition and production separately.
5. Use the learner's preferred large Hanzi and single-sentence translation format for chat practice.
6. After meaningful chat practice, edit `docs/progress.json` and add a short session summary. Do not silently modify the old root-level tracker files.
