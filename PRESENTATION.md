# Presenting script: Mensa Lunch Review (with n8n)

Demo link: https://raw.githack.com/RuoyaoYan/allforbetterfood/913fc6cec19bc4c3b5bd0ae6dbdaa10b108251de/index.html

## Before you start
- **Tab 1:** the demo link. It shows as a phone in the middle of the screen.
- **Tab 2:** n8n with the **Mensa Lunch Review – n8n backend** workflow open in the **Editor**. Press the "fit to screen" button (bottom left, the square corners) so all four sections are visible, like `n8n/workflow-in-n8n.png`.
- Backup: if n8n doesn't load, show `n8n/workflow-in-n8n.png` instead.

## 1. The problem (30 s) · app tab
- Our mensa at Bildungscampus Heilbronn cooks for a very international campus, with a limited set of ingredients.
- The kitchen never hears what students actually liked, so the same unpopular dishes keep coming back.
- Our idea: students review the meal they just ate, and an n8n workflow turns those reviews into a daily report for the kitchen, with dish ideas from around the world.

## 2. The app: Menu page (1 min) · app tab
- The front page shows **today's menu**, one colour band per dish in the colour of the food, with price and vegan/vegetarian labels.
- Each band fills up with how much students loved the dish. About 100 students have reviewed each one today.
- Scroll: **Tomorrow** is a sideways row of cards, so students can plan ahead.
- Scroll: **Yesterday's verdict** ranks yesterday's dishes and flags the ones the kitchen should drop.

## 3. The app: Reviewing (1–2 min) · app tab
- Tap a dish: you jump straight to it on the **Rate** page.
- Reviews are only open 11:00–16:00, because it's a review of today's meal, not a vote on tomorrow's. Press **Open for a demo**.
- Tap **Loved it** on one dish and **Not again** on another. You get a check mark and the count goes up by one.
- Tap the same button again to take the review back. One review per dish per student.

## 4. The app: Kitchen board (1–2 min) · app tab
- Switch to **Kitchen**.
- **Run by n8n** (pink box): the three things the workflow does every day. "Let me show you that workflow in a minute."
- **Stop cooking these:** dishes where at least half of 10+ reviewers said "not again". Today that's the tortellini; yesterday, the mushroom soup and the falafel pan.
- **World kitchen ideas:** press **Suggest dishes from around the world**.
  - Each idea uses ingredients the kitchen already has, lists the few extras to buy, gives the steps and a tip for cooking 300+ portions.
  - Some ideas replace a flopped dish, e.g. a Ghanaian groundnut stew instead of the mushroom soup.
- **Today's reviews** and **Settings** (review window, what counts as a flop).

## 5. The n8n workflow (2 min) · n8n tab
- "The app is just one web page. Everything behind it runs in this n8n workflow."
- Point at the four coloured sections, left to right:
  1. **App data** (green, top left): **App asks for data → Build app data → Send app data**. Every time the app opens, it asks n8n for the menu, the review totals and the AI ideas.
  2. **Reviews** (green, bottom left): **Student reviews a dish → Save review → Send new totals**. Every tap on "Loved it" or "Not again" lands here. n8n checks it's today's meal and inside 11:00–16:00, then updates the shared totals.
  3. **Morning menu** (blue): **Every weekday 06:00 → Fetch OpenMensa menu → Claude: translate dish names → Save English names**. Nobody types the menu: n8n pulls it from the official OpenMensa data and Claude translates it for international students.
  4. **Kitchen report** (purple): **Every weekday 16:05 → Results and prompt → Claude: world dish ideas → Save ideas + build report → E-mail the kitchen**. After lunch, n8n counts the reviews, finds dishes to drop, asks Claude for world dishes made from today's ingredients and e-mails the kitchen.
- Point out the two kinds of triggers: the **clock** icons are schedules (n8n runs them by itself every day), the **webhook** icons are the app calling n8n.
- Optional: double-click **Fetch OpenMensa menu** to show the logic inside, then close it.

## 6. Close (30 s)
- n8n does the daily work automatically: fetching, translating, collecting reviews, counting, reporting.
- Students get heard, the kitchen wastes less food on dishes nobody wants, and an international campus gets dishes from home.
- Next steps: connect a Claude key and Gmail in n8n, switch the workflow on, and pilot it with the Studierendenwerk.

## If something goes wrong
- **No internet:** open `index.html` from the downloaded repo ZIP; show `n8n/workflow-in-n8n.png` for the n8n part.
- **The page looks full-width instead of like a phone:** reload with Option+Command+R or use a private window.
- **Someone asks about the red warning signs on the Claude nodes:** they mean the Claude key isn't added yet in this copy; with a key, those nodes run.
