# Presenting script: Mensa Lunch Review

Demo link (no login): https://raw.githack.com/RuoyaoYan/allforbetterfood/ec5f4ca5b155e27d71ad7f36381756ebc7c54c59/index.html
Offline backup: download this repo as a ZIP and open `index.html`. The menus, sample results and AI ideas are built into the page.

## 1. The problem (30 s)
- Our mensa at Bildungscampus Heilbronn cooks for a very international campus with a limited set of ingredients.
- The kitchen never finds out what students actually liked, so unpopular dishes keep coming back.
- Idea: students review the meal they just ate, and the kitchen gets clear signals plus ideas from around the world.

## 2. Menu page (1 min)
- The front page shows **today's menu**, taken from the official OpenMensa data and shown in English.
- Every dish is a band in the colour of the food: pumpkin orange, curry yellow, beetroot red. You can read it from the queue.
- It shows the opening hours, the category, vegan/vegetarian labels and the student price.
- Scroll: **Tomorrow** is a sideways row of cards, so students can plan ahead.
- Scroll: **Yesterday's verdict** ranks yesterday's dishes by how many people loved them, and flags the ones the kitchen should drop. These numbers are sample data for the demo.

## 3. Rating (1–2 min)
- Tap a dish on the Menu page: you jump straight to it on the **Rate** page.
- Reviews are only open **11:00–16:00**. It's a review of today's meal, not a vote on tomorrow's menu.
- Outside that window, press **Open for a demo** (say: "normally this is only open after lunch").
- Tap **Loved it** on one dish and **Not again** on another. The band fills up as more people love a dish, and your choice gets a check mark.
- Tap the same button again to take the review back. One review per dish per person.

## 4. Kitchen board (2 min)
- Switch to **Kitchen**. This view is for the mensa staff.
- **Stop cooking these:** dishes where at least half of 10+ reviewers said "not again". Yesterday that was the mushroom soup and the potato pan with pumpkin falafel.
- **World kitchen ideas:** AI suggests international dishes that use the ingredients already on today's menu, plus a few pantry basics.
  - Point out: the Ghanaian groundnut stew could replace the mushroom soup; the Turkish bulgur pilaf could replace the falafel pan.
  - Each idea lists what the kitchen already has, what little it needs to buy, the steps, and a tip for cooking 300+ portions.
- **Today's reviews:** a live table of loved vs. not again for each dish.
- **Settings:** staff can change the review window and what counts as a flop.
- **Update a menu:** staff paste the official Speiseplan and AI turns it into dishes (needs an AI key in this version).

## 5. How it's built (30 s)
- Front end only: one HTML page, no server.
- Menu data comes from the OpenMensa API (canteen 277).
- This demo saves reviews on the device. The hosted version shares reviews between all students and asks Claude for live ideas.

## 6. Close (15 s)
- Students get heard, the kitchen wastes less on dishes nobody wants, and an international campus gets food from home.
- Next steps: a real shared database, login via the student card, and a pilot with the Studierendenwerk.
