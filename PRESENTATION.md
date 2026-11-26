# Presenting script: Mensa Lunch Review (with n8n)

Demo link: https://raw.githack.com/RuoyaoYan/allforbetterfood/913fc6cec19bc4c3b5bd0ae6dbdaa10b108251de/index.html

## Before you start
- Open the demo link on your laptop. It shows as a phone in the middle of the screen.
- Put the workflow picture (`n8n/workflow.png`) on a slide, or open it in a second tab.
- No n8n account is needed for the talk. The app runs on its own, and the workflow file in the repo is ready to import whenever someone wants to run it for real.

## 1. The problem (30 s)
- Our mensa at Bildungscampus Heilbronn cooks for a very international campus, with a limited set of ingredients.
- The kitchen never hears what students actually liked, so the same unpopular dishes keep coming back.
- Our idea: students review the meal they just ate, and n8n turns those reviews into a daily report for the kitchen, with dish ideas from around the world.

## 2. How it works (1 min) · show the workflow picture
- The app is just a front end: one web page, no server of our own.
- **n8n is the backend.** Walk through the four lanes:
  1. **App data:** the app asks n8n for the menu, the review totals and the AI ideas.
  2. **Reviews:** every review goes to an n8n webhook, which checks it (today's meal only, 11:00–16:00) and updates the shared totals.
  3. **Morning menu:** every weekday at 06:00, n8n fetches the official menu from OpenMensa and Claude translates it into English.
  4. **Kitchen report:** every weekday at 16:05, n8n counts the results, finds dishes to drop, asks Claude for world dishes and e-mails the kitchen.

## 3. Menu page (1 min)
- Back in the app: the front page shows **today's menu**, one colour band per dish in the colour of the food, with price and vegan/vegetarian labels.
- Say: nobody typed this menu. n8n fetched it from the official OpenMensa data this morning, and Claude translated it for international students.
- Each band fills up with how much students loved the dish. About 100 students have reviewed each one today.
- Scroll: **Tomorrow** is a sideways row of cards, so students can plan ahead.
- Scroll: **Yesterday's verdict** ranks yesterday's dishes and flags the ones the kitchen should drop.

## 4. Reviewing (1–2 min)
- Tap a dish: you jump straight to it on the **Rate** page.
- Reviews are only open 11:00–16:00, because it's a review of today's meal, not a vote on tomorrow's. Press **Open for a demo**.
- Tap **Loved it** on one dish and **Not again** on another. You get a check mark, and the count goes up by one.
- Tap the same button again to take the review back. One review per dish per student.
- Say: each tap is sent to n8n's **Reviews** lane (point at it on the workflow picture).

## 5. Kitchen board (2 min)
- In the app: **Kitchen**.
- **Run by n8n** (pink box): the three things the workflow does every day.
- **Stop cooking these:** dishes where at least half of 10+ reviewers said "not again". Today that's the tortellini; yesterday, the mushroom soup and the falafel pan.
- **World kitchen ideas:** press **Suggest dishes from around the world**. The ideas come from the **Kitchen report** lane: n8n hands today's ingredients and the flopped dishes to Claude.
  - Each idea uses ingredients the kitchen already has, lists the few extras to buy, gives the steps and a tip for cooking 300+ portions.
  - Some ideas replace a flopped dish, e.g. a Ghanaian groundnut stew instead of the mushroom soup.
- On the workflow picture, point at **E-mail the kitchen**: after lunch the kitchen gets this report automatically.
- **Today's reviews:** loved vs. not again for every dish.
- **Settings:** staff set the review window and what counts as a flop.

## 6. Close (30 s)
- n8n does the daily work: fetching, translating, collecting reviews, counting, reporting.
- Students get heard, the kitchen wastes less food on dishes nobody wants, and an international campus gets dishes from home.
- Next steps: a proper database inside n8n, login with the student card, and a pilot with the Studierendenwerk.

## If something goes wrong
- **No internet:** open `index.html` from the downloaded repo ZIP. Menus, reviews and ideas are built in.
- **The page looks full-width instead of like a phone:** reload with Option+Command+R or use a private window.
- **Someone asks if n8n really runs it:** the workflow file is in the repo (`n8n/mensa-lunch-review.workflow.json`); import it into n8n, add a Claude key and activate it, then connect the app under Kitchen → Settings.
