# Presenting script: Mensa Lunch Review (with n8n)

Demo link: https://raw.githack.com/RuoyaoYan/allforbetterfood/913fc6cec19bc4c3b5bd0ae6dbdaa10b108251de/index.html

## Before you start
- Open the demo link on your laptop. It shows as a phone in the middle of the screen.
- Connect n8n once: **Kitchen → Settings → n8n webhook URL → Connect**. The pink **Run by n8n** box should then say "Live".
- Open n8n in a second tab with the **Mensa Lunch Review – n8n backend** workflow (activated), and keep the **Executions** list ready.
- Press **Suggest dishes from around the world** once beforehand, so fresh ideas are already there.

## 1. The problem (30 s)
- Our mensa at Bildungscampus Heilbronn cooks for a very international campus, with a limited set of ingredients.
- The kitchen never hears what students actually liked, so the same unpopular dishes keep coming back.
- Our idea: students review the meal they just ate, and n8n turns those reviews into a daily report for the kitchen, with dish ideas from around the world.

## 2. How it works (30 s)
- The app is just a front end: one web page, no server of our own.
- **n8n is the backend.** Switch to the n8n tab and point at the four sections:
  1. **App data:** gives the app the menu, the review totals and the AI ideas.
  2. **Reviews:** receives every review.
  3. **Morning menu:** every weekday at 06:00, gets the menu and translates it.
  4. **Kitchen report:** every weekday at 16:05, counts the results, asks Claude and e-mails the kitchen.

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
- Switch to n8n → **Executions**: every tap is a run of **Student reviews a dish → Save review → Send new totals**.

## 5. Kitchen board (2 min)
- In the app: **Kitchen**.
- **Run by n8n** (pink box): what the workflow does every day, and live, how many reviews n8n received today and what it last did.
- **Stop cooking these:** dishes where at least half of 10+ reviewers said "not again". Today that's the tortellini; yesterday, the mushroom soup and the falafel pan.
- **World kitchen ideas:** press **Suggest dishes from around the world**. The app calls n8n, n8n asks Claude, and about 30 seconds later the ideas appear. Meanwhile, show the run in n8n: **Results and prompt → Claude: world dish ideas → Save ideas + build report**.
  - Each idea uses ingredients the kitchen already has, lists the few extras to buy, gives the steps and a tip for cooking 300+ portions.
  - Some ideas replace a flopped dish, e.g. a Ghanaian groundnut stew instead of the mushroom soup.
- In n8n, point at **E-mail the kitchen**: after lunch the kitchen gets this report automatically.
- **Today's reviews:** loved vs. not again for every dish.
- **Settings:** staff set the review window and what counts as a flop.

## 6. Close (30 s)
- n8n does the daily work: fetching, translating, collecting reviews, counting, reporting.
- Students get heard, the kitchen wastes less food on dishes nobody wants, and an international campus gets dishes from home.
- Next steps: a proper database inside n8n, login with the student card, and a pilot with the Studierendenwerk.

## If something goes wrong
- **n8n not reachable:** the app still works on its own. Reviews save on the laptop and prepared AI ideas show. Explain the n8n part from the workflow screen.
- **No internet:** open the downloaded `index.html` from the repo ZIP. Menus, reviews and ideas are built in.
- **The page looks full-width instead of like a phone:** reload with Option+Command+R or use a private window.
