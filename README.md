# Prompt G public JSON feed

This repository supplies public Prompt G research to [Live Session Desk](https://live-session-desk-m.aditity21212.chatgpt.site/).

The read-only feed is [live-events.json](https://raw.githubusercontent.com/thesadist60-create/prompt-g-feed/main/live-events.json). Visitors read it without GitHub credentials. The Site validates it on page load and every minute while open, and uses its bundled JSON as fallback if fetching or validation fails.

## Publishing a research run

Use the authenticated GitHub connection to replace `live-events.json` on `main`. Read its current blob SHA before updating and use that SHA to guard against concurrent writes. Read the public raw feed back to verify the update. A routine data update takes one file commit.

The root object uses `version: 1`, `window: {startUtc, endUtc}`, `updatedAtUtc`, and `events`. Timestamps use exact ISO UTC strings ending in `Z`. Preserve the actual research time in `updatedAtUtc` and each evidence check time in `checkedAtUtc`. `feedRevision` is optional transport metadata and never changes the research timestamp. Each event needs an occurrence ID, title, organizer, category, start/end (null when unknown), platform, public source URL, verification, access route, and cost state. The Site’s `dist/live-data.mjs` defines the full validation contract. Its `PROMPT_G_PUBLISHING.md` contains the research and publication procedure.

The initial feed copies the Site’s existing 71 records with their original research time. It does not establish new occurrences or current admission. Elapsed events are hidden by the Site automatically. Publish only documented public source and access information.
