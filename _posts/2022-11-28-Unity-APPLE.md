---
title: "Applying A.P.P.L.E. to Unity"
date: 2022-11-28
---

## Introduction
A.P.P.L.E. (APPLE) is an acronym for customer service techniques used by [Apple Inc.](https://de.wikipedia.org/wiki/Apple) employees. [Here is an explanation from 2011](https://www.socialmediatoday.com/content/apples-customer-service-secrets-revealed-apple). This acronym will be applied to Unity development here. Applying APPLE to Unity is inspired by the [writings of mitchellh](https://mitchellh.com/writing/apple-the-key-to-my-success).

When I worked my first real job a senior backend developer reminded me to always be aware of who the "customer" for my code was: was it a bank? How many players would rune this code - 10 or 10 million? Will many other developers see this code? These questions helped me to always consider the quality and requirements of my code.

## Method
Each of the points will be viewed from different perspectives as they relate to Unity.
Unity Editor: Consider editor users as the customer.
Unity Code: Consider yourself and other developers as the customer.
Unity games: Consider your players as the customer.

Below a table summary:
| Unity Case |  Customer |
|---|---|
| Unity Editor | User of the editor |
| Unity Code  | Developers of the project  |
| Unity Build | Players of the game  |

## Results
**A**pproach customers with a personalized warm welcome.
Unity Editor: It can be nice to have a logo: e.g. the DoTween Utility panel does this.
Unity Code: It can be nice to have class comments and to introduce new developers to the codebase in 1-on-1 meetings.
Unity Game (Build): Nowadays (2022) mobile Unity games tend to have tutorials which allow players to choose their names and equipment. An example of this  is "Harry Potter: Puzzles & Spells" (Zynga, 2020) where players can select their name and wands when starting their wizarding journey.

**P**robe politely to understand all the customer’s needs.
Unity Editor: Hold a meeting with game designers to find out what they want.
Unity Code: Define types were specifically so that their usage may be more easily understood (Inform rather than ask needs).
Unity Game (Build): Ask players for feedback when their activity seems to decrease (e.g. based on analytics tracking).

**P**resent a solution for the customer to take home today.
Unity Editor: Find quick fixes to unblock the work of developers and designers using the tools.
Unity Code: Find small steps (rather than quick fixes) which take the codebase in the right direction. Right could be based on developer votes (e.g. for topics like naming, architecture, etc.)
Unity Game (Build): Find quick fixes to unblock players and offer them compensation rewards (e.g. soft currency).

**L**isten for and resolve any issues or concerns.
Unity Editor: Listen to reoccuring issues brought up by those that use the editor the most (e.g. "this takes forever to load", "my editor keeps crashing", etc.)
Unity Code: Code reviews are a source where other developers will provide concerns feedback. Listen to them and remember them for future reviews.
Unity Game (Build): Players use the app stores (e.g. Google Play) to give feedback, listen to these issues, especially if they don't show up in your testing (e.g. untraceable network issues).

**E**nd with a fond farewell and an invitation to return.
Unity Editor: N/A?
Unity Code: Classes should leave a nice aftertaste, almost asking to be extended. That way developers will like to come back. One of doing this is by avoiding boilerplate to create more "empty space" in the class.
Unity Game (Build): Add an "offboarding" for players who uninstall the game, letting them know they will get a reward when they come back or something similar.

Further similarities:
- consider Apple's customer support as your company's Slack channel where game designers ask other developers for help with the tools
- consider "invitation to return" (E) as your company's retrospective (assuming an agile workflow) where issues may be discussed

## Limitations
Because no equivalency between Unity and APPLE has been expressed there will likely be differences. For example, it is unclear whether personalization would provide a benefit with a Unity editor used by many different people.