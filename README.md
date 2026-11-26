# All for better food: Mensa Lunch Review

A front-end-only app for **Mensa am Bildungscampus Heilbronn** (Studierendenwerk Heidelberg).

- **Rate:** students review today's meals ("Loved it" / "Not again") during a review window (default 11:00–16:00, Berlin time). Each dish is a band in the colour of the food, and it fills up as more people love it.
- **Kitchen:** staff see which dishes to stop cooking (at least 50% "not again" from 10+ reviews, adjustable), today's results, and AI suggestions for international dishes that can be made from the ingredients already on the menu, for an international campus.

## Pages

- **Menu (front page):** today's dishes as colour bands (tap one to rate it), tomorrow's menu, and yesterday's verdict, i.e. how each dish was rated.
- **Rate:** reviews are open 11:00–16:00. Outside that window, use **Open reviews for a demo** to try voting.
- **Kitchen:** stop-cooking list, AI world-dish ideas, today's results, settings and menu upload.

The results for Wed 25 Nov in `samples.json` are **made-up sample data** for demos. The page labels them as such.

## Running it

It's a single static `index.html`, with no build step and no backend.

- **GitHub Pages / any static host (standalone mode):**
  - The menu loads live from the [OpenMensa API](https://openmensa.org/api/v2/canteens/277/meals). `menu.json` is a saved fallback copy.
  - Reviews and settings are saved in the browser (`localStorage`), so each device sees only its own reviews.
  - For AI ideas and menu reading, staff paste an Anthropic API key under Kitchen → Settings. It's kept only in that browser.
- **Claude artifact (hosted mode):** when the page runs inside Claude, it uses Claude's shared storage, so reviews are shared by everyone, and Claude handles the AI suggestions.

## Files

- `index.html`: the whole app
- `menu.json`: saved menu copy used if OpenMensa can't be reached
