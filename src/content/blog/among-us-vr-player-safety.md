---
title: Designing Among Us VR’s Player Safety Solution
author: Mack Nelson
pubDatetime: 2023-09-30T04:06:31Z
postSlug: among-us-vr-player-safety
featured: false
tags:
  - player-safety
  - design
  - gaming
  - figma
  - toxmod
description: Some writings of the my work on the design of Among Us VR's Player Safety Solution.
---
![Cover image for article regarding player safety in Among Us VR](https://cdn.vandraworks.com/mackportfolio/web-portfolio-mockup_11-min.png)

Among Us VR - the virtual reality reimagining of perhaps the pandemic’s hottest viral gaming sensation - was a few months away from launch. As I sat wrapping up work on the schellgames.com revamp, an email landed into my inbox.

_“For \[Among Us VR]: We're going to need to write a backend for user reporting that takes in events from the Airlock game and writes out tickets. Do you happen to know of a contractor that we might be able to use to write such a thing?”_

This seemed like a straightforward request, but the context is important. The events described in the email would become user-generated reports, which required backend infrastructure to support as well as a front-end for player safety agents to sift through and act upon. We quickly realized that we lacked this infrastructure, only a few months away from launch. The Among Us VR player safety project was born shortly after this realization.

Among Us VR was Schell Games’ first major foray into online multiplayer experiences of this scale. We were far behind in terms of implementing player safety, and we needed to catch up as soon as possible. However, we also wanted to ensure that our implementation would stand the test of time - and volume. This forced me to balance two immediate and classic stakeholder priorities internally - time to market and quality of our final product.

My responsibilities included designing the support agent panel and general product management duties, such as developing the product roadmap and managing the workload of the contractors who developed the app. However, this case study will focus on my design duties for the project.

**Internal Alignment**

The first immediate step was to identify, align, and keep aligned, our internal stakeholders so that we could develop a list of priorities and specs for the panel as well as continue iteratively gathering feedback and ideas as the design took shape. Consistently aligning product people, support agents, and developers - all in the final, hectic months of development - became a major challenge. Through prioritizing async communication and squeezing in important syncs where we could (including a catered design sync during lunchtime), we were able to keep our internal stakeholders closely engaged with the status of the project, while at the same time not interfering with their busy pre-launch schedules. We also were able to naturally discover many unknown constraints (technical, legal, or otherwise) through repeated syncs and communication across the team at large.

**External Insight**

Additionally, I wanted to ensure that I got enough input from our close external partners on the design of the tool in order to find any potential unknowns as well as gather usage insights on similar tools in the player safety space (few as they may be!).

Innersloth, the creators of the original Among Us title, went through a similar player safety overhaul. Because their game and our game likely would have extremely similar playerbases and therefore player safety challenges, I wanted to gather as much insight from their team (as well as ensure that we weren’t needlessly reinventing the wheel).

Schell Games also partnered with Keywords, a major video game services company in order to provide player support assistance. Part of my design process was keeping in close contact with our partners at Keywords. As their agents would be the ones most closely interacting with the tool, and seeing as though they likely had experience with other tools similar to the one we were building, I wanted to make sure that their input was as highly valued as some of our internal stakeholders. Their insight provided us with loads of additional considerations and edge cases (what happens to a support agent’s active tickets when they go offline, or get sick?)

![Two early sketches of the Player Safety app for Among Us VR](https://cdn.vandraworks.com/mackportfolio/Frame%201-min.jpg)

**Cognitive Load**

One recurring priority ran throughout our conversations with our external partners and internal stakeholders. - speed. Specifically, the speed at which an agent can work through a report in our system. We expected hundreds of thousands of players in our first week, with 1 to 4 percent of them submitting at least one report; a queue of player reports could quickly balloon into the tens of thousands. Designing a system which allowed agents to get through a player report in the quickest time possible was very important.

We also realized, especially through our conversations with the folks at Keywords, that having to listen to highly toxic behaviors day in and day out is quite a stressful job indeed. It quickly became important to us to decrease the exposure to toxicity on an agent as much as we reasonably could (which had the added benefit of aligning with quickly dealing with reports).

With these two realizations in mind, reducing the overall cognitive load on a support agent at any given time became a guiding principle for me while designing the tool (_“Player safety, agent sanity”)_, and led to the two foundational pieces of our player safety app.

**The Batch Queue System**

It’s been proven that taking massive datasets and turning them into smaller and more manageable chunks reduces the cognitive load on the brain. For this reason, we developed the “Batch Queue” system - a way for support agents to get small, manageable batches of reports from the database instead of immediately being confronted with a virtually infinite list of infractions. This also allowed agents to “own” reports, eliminating the likelihood of two agents getting the same report.

![Image of the Queue View](https://cdn.vandraworks.com/mackportfolio/Queue%20%28Pre-Chunk%29%20%282%29-min.png)

**The Player Card**

Alright, we’ve got a way for agents to chip away at the queue of individual reports - but we’ve still got thousands of potential reports coming in every week. Not manageable. What other ways do we have of reducing the amount of reports in the queue? Additionally, we can make an assumption that a lot of players that break the rules will be repeat offenders. What if two players report the same suspect for the same infraction? How can we mark that as a duplicate?

Through one of our design syncs came the answer to that question - the Player Card.

![Image of Queue system at work](https://cdn.vandraworks.com/mackportfolio/Queue%20-%20Card%20%28Incident%20Review%29%20%281%29-min.png)

Instead of displaying individual reports to a support agent and then handing out bans based on those individual infractions, we instead decided to group together all existing infractions that a player has accrued and then display all of them at once to a support agent. Immediately, we have drastically reduced the overall “items” in the queue - from tens of thousands of reports to thousands of player cards.

This design also provides support agents with much more context than if the app were to just provide an individual report. Each Player Card includes a high-level summary of a player’s infraction history, including:

1. Amount of open incident reports filed against them, and a summary of those incidents
2. Previous closed incident history
3. Previous bans
4. Account age/account creation date

This should quickly allow the support agent to make context-driven decisions on punishments.

**Prioritizing Problem Players**

Each infraction has a category (from smaller offenses like griefing, to more serious offenses, such as sexual harassment). How do we ensure that the most egregious and repeat offenders are dealt with quickly?

We developed a priority point system to solve this problem. In the back-end, each infraction category has an associated priority point value. The combined total of these priority points help to determine just how much importance a player card should have in the queue. Additional factors include:

- Combined age of incidents (the older the age of incidents, the higher the priority)
- Repeat offenders
- Manually flagged players

**Risk-Averse Design**

Unknowns are part of many projects, especially ones of this scale - but this project included one very major unknown that needed to be accounted for.

ToxMod, an AI/ML-powered moderation suite for games, came into the picture about a quarter of the way through our design process. We weren’t yet sure whether we were going to incorporate their tool into our overall design strategy, but we didn’t have the luxury of designing for multiple outcomes. Instead, we created a Player Card design that could incorporate the reports that ToxMod would generate automatically right alongside the existing list of reports generated by players.

**Quick Iterations**

“Nothing good is designed in a bubble”.

I find that the most foolproof way to good design is repeated iteration. Generally, the more times I can get the eyes of others - be it stakeholders, users, or other designers - to look at what I’m doing - the easier it is for me to arrive at the solution that makes the most sense. We used this to great effect on this project - through our design sync process, as well as our commitment to continuous asynchronous feedback and not being afraid to show very clearly incomplete work - we were able to simplify the scope of our project by 35% by removing an entire section of the app and adding the required functionality of that app to our existing Player Card functionality.

**Handing Off**

Eventually, my work on the player safety team came to an end - and it came time to hand off my design work to the Design Director of the project as I returned to my normal duties within Marketing. Through a commitment to consistent documentation (both with an evergreen Product Brief/Design Doc, a User Manual to help describe functionality from the Support Agent perspective, as well as contextual comments on the design itself), the handoff was simple, with minimal need for project walkthroughs or other resources spent clarifying my work on the project.

**Results**

The Player Safety Update launched as part of Among Us’ VR’s 5th patch in April of 2023. To date, the system has successfully dealt with tens of thousands of infractions and has dealt bans out to thousands of players. The tool continues to see improvements and changes alongside our integration with ToxMod.

Want to know more about my design experience on this project, or about my other responsibilities on the player safety team? [Email Me](mailto:hi@macknelson.com).
