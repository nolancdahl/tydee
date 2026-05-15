# Tydee

A personal cleaning chore rotation app. Press a button, get three chores to do today, grouped by proximity in the house and ranked by how overdue they are.

## How it works

Each chore has an ideal cadence (e.g. clean toilet every 7 days, descale tea kettle every 56 days). The app scores chores by `days_since_last_done / ideal_cadence` so the most overdue chore floats to the top regardless of category. The other two slots are filled with chores in the same zone, then the same floor, then anywhere else.

## Color coding (Last Done column)

- **Green** — fresh (0-74% of cadence elapsed)
- **Yellow** — due soon (75-99%)
- **Red** — overdue (100%+)
- **Gray dash** — never logged

## Local development

It's a single HTML file. Open it in any browser:

```
open index.html
```

No build step, no dependencies, no package manager.

## Deployment

Auto-deploys to Netlify on every push to `main`.

## Data storage

History persists per-device via `localStorage`. There's no cross-device sync yet — marking "Done" on the phone won't show up on the desktop and vice versa. Use one device as the source of truth, or add a backend (e.g. Supabase) for sync.

## Editing the chore list

The chore list lives in the `CHORES` array near the top of the `<script>` block in `index.html`. Each entry has:

- `id` — unique identifier (don't change once data is logged)
- `name` — display name
- `zone` — grouping bucket (e.g. "3rd Bathroom")
- `floor` — 1, 2, or 3 (for proximity fallback)
- `mins` — estimated minutes
- `tools` — comma-separated tools, each like `"tool name (location)"`
- `freq` — ideal cadence in days
