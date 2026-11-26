# Presenting script: Mensa Lunch Review (with n8n)

Demo link: https://raw.githack.com/RuoyaoYan/allforbetterfood/183d08f00f6fdcde18063b3f6204efa1d1dc5644/index.html

**Before you start**
- Open the demo link and connect n8n once: Kitchen → Settings → n8n webhook URL → Connect. The footer of the Kitchen page should say "Connected to n8n".
- Open n8n in a second tab with the **Mensa Lunch Review – n8n backend** workflow, and keep the **Executions** list ready.
- Optional: have a second device open the same link, to show that reviews are shared.

## 1. The problem (30 s)
- The Bildungscampus mensa cooks for a very international campus with limited ingredients.
- The kitchen never hears what students liked, so unpopular dishes keep coming back.
- Our idea: students review the meal they just ate, and n8n turns those reviews into a daily kitchen report with ideas from around the world.

## 2. Architecture in one sentence (30 s)
- The app is only a front end: one HTML page, no server of our own.
- **n8n is the backend.** One workflow with four parts serves the menu, stores the reviews, talks to Claude and e-mails the kitchen.
- Switch to the n8n tab and point at the four coloured sections: App data · Reviews · Morning menu · Kitchen report.

## 3. Morning menu, automated (1 min)
- In n8n: **Every weekday 06:00** → **Fetch OpenMensa menu** → **Claude: translate dish names** → **Save English names**.
- Say: nobody types the menu. n8n pulls the official data from OpenMensa and Claude translates it for international students.
- Optional live demo: open the `…/webhook/mensa-refresh` URL, then show the new execution in **Executions**.

## 4. Menu page (1 min)
- Back in the app: the front page shows **today's menu**, one band per dish in the colour of the food, with price and vegan/vegetarian labels.
- Scroll: **Tomorrow** is a sideways row of cards.
- Scroll: **Yesterday's verdict** ranks how much each dish was loved and flags the ones to drop.

## 5. Reviewing (1–2 min)
- Tap a dish: you jump to it on the **Rate** page.
- Reviews are only open 11:00–16:00, because it's a review of today's meal. Press **Open for a demo**.
- Tap **Loved it** on one dish and **Not again** on another. The band fills up as more people love it.
- Switch to n8n → **Executions**: each tap ran **Student reviews a dish → Save review → Send new totals**.
- Optional: vote on the second device, and the first device's numbers go up within 30 seconds. The reviews are shared through n8n.

## 6. Kitchen board + AI (2 min)
- In the app: **Kitchen**. The pink **Run by n8n** box at the top shows what the workflow does every day, and (when connected) its live activity and how many reviews n8n received today.
- **Stop cooking these**: dishes where at least half of 10+ reviewers said "not again", e.g. today's tortellini and yesterday's mushroom soup and falafel pan.
- Press **Suggest dishes from around the world**. The app calls n8n, and n8n runs **Results and prompt → Claude: world dish ideas → Save ideas + build report**. The ideas appear after about 30 seconds.
- Point out: each idea uses ingredients the kitchen already has, lists what little to buy, gives the steps and a tip for 300+ portions, and can replace a flopped dish.
- In n8n: show **Every weekday 16:05** and **E-mail the kitchen**. After lunch, the kitchen gets this report by e-mail automatically.

## 7. Settings (15 s)
- Staff can change the review window and what counts as a flop.

## 8. Close (30 s)
- n8n does the boring work every day: fetching, translating, counting, reporting. The app stays a simple page.
- Students get heard, the kitchen wastes less food, and an international campus gets dishes from home.
- Next steps: move the storage to a real database (n8n Data Tables or Postgres), log in with the student card, and pilot with the Studierendenwerk.

**If n8n is down during the talk:** the app keeps working on its own. Reviews save on the laptop, and the prepared AI ideas still show.
