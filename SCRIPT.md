# Word-for-word script: Mensa Lunch Review

*About 7 minutes. [Brackets] are actions, not spoken.*

---

**[App tab open, Menu page]**

Have you ever stood in the mensa queue, looked at the menu and thought: seriously, fried fish *again*?

Same dry fish, same sad sauce, every week. And you eat it anyway, because it's two euros and you have a lecture in twenty minutes.

But here's the thing: nobody in the kitchen ever finds out you hated it. So next week, guess what's back?

**[pause, let them answer]**

The fish.

And it's not just about taste. Our campus is really international: students from India, China, Turkey, Africa, Latin America. But the mensa works with a limited set of ingredients, and it has no idea what we actually like.

So we built an app that lets the mensa finally listen. You rate today's lunch in ten seconds. And every afternoon, an n8n workflow tells the kitchen what to stop cooking and what to cook instead, with dishes from all around the world.

Let me show you.

---

**[Menu page]**

This is the front page. It shows today's menu from our mensa at Bildungscampus, Thursday the 26th.

Every dish is a band in the colour of the food: orange for the pumpkin curry, red for the beetroot soup, brown for the burger. You see the price, and whether it's vegan or vegetarian.

The darker part inside each band shows how much students loved the dish. About a hundred students have already reviewed each one today. And the menu is in English. The official one is only in German, so for a lot of us that already helps.

**[scroll down]**

Down here is tomorrow's menu, so you can plan ahead. Tomorrow it's sushi from the food truck.

**[scroll down]**

And this is yesterday's verdict. French fries, ninety-one percent loved it, no surprise. But down here: the mushroom soup and the potato pan with pumpkin falafel. More than sixty percent of students said "not again". So the app flags them: the kitchen should drop these.

---

**[tap a dish → Rate page]**

Now, how do you review? I tap a dish, and it takes me straight to the rating page.

One important thing: reviews are only open from eleven to four. This is not a vote on what to cook tomorrow. It's a review of the meal you just ate. Right now it's evening, so I'll open it for the demo.

**[press "Open for a demo"]**

I had the Thai curry today. I loved it.

**[tap "Loved it" on the Thai curry]**

There's my check mark, and the count goes up by one. The tortellini, on the other hand...

**[tap "Not again" on the tortellini]**

Not again. If I change my mind, I just tap again and it's gone. One review per dish per student, so nobody can spam it.

---

**[tap Kitchen]**

So that's the student side. This is the kitchen side.

At the top, in pink: Run by n8n. This is what our workflow does for the kitchen every single day. I'll show you the workflow itself in a minute.

**[scroll to "Stop cooking these"]**

Here's the list the kitchen really needs: Stop cooking these. Any dish where at least half of ten or more students said "not again" lands here. Today, that's the tortellini. Yesterday, the mushroom soup and the falafel pan.

But just telling the kitchen "this is bad" doesn't help much. They need to know what to cook instead, with the ingredients they already have.

**[press "Suggest dishes from around the world"]**

So we ask AI. It looks at today's ingredients — pumpkin, rice, bulgur, beetroot, tomatoes, pak choi — and suggests dishes from around the world.

**[scroll through the ideas]**

A Ghanaian groundnut stew, made from the pumpkin and tomatoes. It could replace the mushroom soup. A Turkish bulgur pilaf to replace the falafel pan. Ukrainian borscht from the beetroot. Chinese garlic pak choi with mushrooms. And Mexican chicken tinga.

For every dish, the kitchen sees what they already have, the few extra things to buy, the steps, and a tip for cooking three hundred portions. And for students from those countries, it's a taste of home.

---

**[switch to the n8n tab, workflow fitted to screen]**

Now, the part that makes all of this run: n8n.

The app itself is just one web page. It has no server. Everything behind it is this one n8n workflow, and it has four parts.

**[point at "1 · App data"]**

Part one, App data. Every time someone opens the app, it asks n8n for the menu, the review totals and the AI ideas, and n8n sends them back.

**[point at "2 · Reviews"]**

Part two, Reviews. Every time I tapped "Loved it" or "Not again", it landed here. n8n checks that it's today's meal and that it's between eleven and four, then updates the totals for everyone.

**[point at "3 · Morning menu"]**

Part three, the morning menu. See the clock? Every weekday at six in the morning, n8n fetches the official menu from OpenMensa, and Claude translates it into English. Nobody has to type anything.

**[point at "4 · Kitchen report"]**

And part four, the kitchen report. Every weekday at five past four, right after reviews close, n8n counts the results, finds the dishes to drop, asks Claude for world dishes made from today's ingredients, and emails the full report to the kitchen.

**[point at a clock icon, then a webhook icon]**

There are two kinds of starting points. The clocks run by themselves every day. The webhooks are the app talking to n8n. So once it's switched on, nobody has to do anything. It just runs.

---

**[back to the app tab, or stay on n8n]**

So, to sum up.

Students get heard: ten seconds after lunch, and your opinion actually reaches the kitchen.

The kitchen gets a clear list every afternoon of what to drop, and real ideas for what to cook instead, using what they already have.

And n8n does all the boring work automatically: fetching the menu, translating it, collecting the reviews, counting, and reporting.

Our next steps: connect it to the student card for login, and pilot it with the Studierendenwerk.

Because nobody should have to eat that fried fish again.

Thank you.

---

*If something breaks:*
- *n8n won't load:* "Here's a screenshot of the workflow." Show `n8n/workflow-in-n8n.png`.
- *Someone asks about the red warning icons on the Claude nodes:* "Those just mean the AI key isn't added in this copy yet. With a key, those steps run."
