# n8n backend for Mensa Lunch Review

`mensa-lunch-review.workflow.json` is a ready-to-import n8n workflow. It turns the front-end-only page into a shared app: one place that keeps the menu, everyone's reviews and the AI ideas.

## What the workflow does

| Part | Trigger | What happens |
|---|---|---|
| 1 · App data | `GET /webhook/mensa?uid=…` | Sends the page the menus, the shared review totals, the viewer's own reviews and the latest AI ideas. Loads the menu from OpenMensa if today's is missing. |
| 2 · Reviews | `GET /webhook/mensa-vote?uid=&date=&key=&v=` | Saves one review per dish per student. Only accepts today's meal, and only between 11:00 and 16:00 (or with `demo=1`). |
| 3 · Morning menu | Every weekday 06:00, or `GET /webhook/mensa-refresh` | Fetches the week's menu from OpenMensa (canteen 277). Claude translates new dish names into English. |
| 4 · Kitchen report | Every weekday 16:05, or `GET /webhook/mensa-ideas` (the app's "Suggest dishes" button) | Counts today's reviews and finds the dishes to drop. Asks Claude for 5 world dishes made from today's ingredients, saves them for the app and e-mails the kitchen. |

Data lives in the workflow's static data, so there's no database to set up. n8n only saves static data on production runs, so test with the workflow **activated**.

## Setup (about 5 minutes)

1. In n8n: **Workflows → Import from File** → choose `mensa-lunch-review.workflow.json`.
2. Open **Claude: translate dish names** → Credential → *Create new* → **Header Auth**. Set Name to `x-api-key` and Value to your Anthropic API key. Pick the same credential in **Claude: world dish ideas**.
3. Optional: open **E-mail the kitchen**, connect Gmail, set the address, and enable the node.
4. **Activate** the workflow (switch at the top right).
5. Open **App asks for data** and copy the **Production URL**, e.g. `https://you.app.n8n.cloud/webhook/mensa`. Remove `/mensa` from the end.
6. In the app: **Kitchen → Settings → n8n webhook URL**, paste it, and press **Connect**. Or put it in `index.html`: `<meta name="n8n" content="https://you.app.n8n.cloud/webhook">`.
7. Open `https://…/webhook/mensa-refresh` once in the browser to load and translate this week's menu.

## Notes

- The Claude nodes use the model `claude-sonnet-5-5`. If they fail, the app still works: names stay in German and the ideas fall back to the prepared ones.
- Two reviews arriving at the same instant can overwrite each other in static data. That's fine for a demo; for real use, swap the storage for n8n Data Tables, Google Sheets or Postgres.
