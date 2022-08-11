---
title: "Perfection is your enemy, on Unity project architecture"
date: 2022-08-11
---

## Why?
I am on vacation in Belgium right now, thinking a lot about time, especially because I am watching my half-siblings (who are now 6 and 7) grow up very quickly. They are not building their LEGOs perfectly but they are definitely getting finished. Games need to be finished too, or at least released, to be playable by the player base. That means shortcuts need to be made because a perfect project architecture would take forever. This post is about these types of shortcuts.

## Imperfect Shortcuts
these are roughly speaking the rules I go by for personal and professional work. Take them with a grain of salt.

**Never reinvent the wheel if you have a deadline.**

For example, do not write your own networking library and do not create your own HTML UI canvas inside of Unity. It will probably cost your more time to bugfix it than you expect. Another example: I remember a student was delayed with his work because he had a bug in his tweening library, fixing his library meant he had to delay the gameplay fixes related to quests in his game.

My tip: use existing libraries, e.g. DoTween, UniRx, Odin Inspector, etc.

**Copy & Paste code, especially if you don't know how it will change in the future.**

This may sound odd at first. You may remember some developers calling duplication the root of all evil. Let me give you a spexific example.

An example: UI is constantly changing in games; the UX flow is getting redesigned, notification bubbles are added, icons are changing, etc. A lot of this behavior is defined in MonoBehaviors. At first a `AttackButton` and a `SettingsButton` might each have one click action and that's it. However, as they evolve there might be a notification bubble for each. The conditions for these bubbles will probably be different (e.g. `AttackButton` will show notifications if an attack can be made and the `SettingsButton` will show notifications if new account features are unlocked). As this behavior diverges further and further it will be difficult to maintain it under one class. In fact, it will go against the single-responsibility-principle: one class is suddonly containing logic for two separate topics: settings and attacks.

My tip: Create one `AttackButton` class and one `SettingsButton` class. To reduce at least some of the duplicated code I often use extensions to wrap behavior like `button.onClick.AddListener(Callback)` and also remove existing listeners.

**Use an engine and version you are familiar with**
Anyone who has been making games long enough will probably remember that one project where they tried to upgrade to the latest Unity beta version. Or the project where they tried out a different engine, like Godot, event though none of the developers had worked with it before. These choices do not doom a project by themselves but they can increase the difficulty of making progress.

If I start a new project nowaways for release I will use the penultimate LTS version. So if 2021 LTS is the latest LTS then I will use 2020 LTS. This is because even an LTS can have annoying bugs. A specific example: Unity LTS 2021.3.4f1 has problems serializing serialzable structs which I was using for audio configs. This made every day tasks like changing sound effects tedious because sometimes the editor would glitch and the reference would need to be set again. Now imagine you are one a team with 20 other people and they are all struggling against the editor. 

My tip: use a version that is stable and familar for the team. It may not have all of the latest feature (and maybe not even all of the latest bugfixes) but there's a good chance it will save you some trouble.

## Limitations
For personal project you may want to break these rules on purpose. For example, writing your own UniRx clone may teach you more about how these sort of library might work internally.

---
 That's it.