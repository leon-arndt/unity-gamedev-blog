---
title: "Game Data Identification"
date: 2023-08-24
---

# Game Data Identification
Some different approaches to structuring IDs, e.g. "Lvl1_EnemyMelee_01"
1. Every ID is a descriptive string
2. Every ID is a generated string (e.g. Unity GUID)
3. Every ID is in int (e.g. an enum)
4. Every ID is an object (pass by value)

## Every ID is a descriptive string
This approach has some benefits:
1. Names are closely connected to their values
2. Renaming should be easy (e.g. use `rg` in terminal to find all usages)

It also has some drawbacks:
1. Naming consistency is hard to enforce "Lvl1" vs "LVL1" vs "Level_01" are arbitry.
2. In some cases the serialization could be a lot bigger than the generated string. E.g. `Lvl1_EnemyMelee_01_WinterIntroCutscene` is longer than `923a1a0c`. This depends on how short your guids are, e.g. `923a1a0c-bfff-4eec-b567-f3727571edc8` is longer but you might now need all those permutations to represent your game's data. There are strong similarities to referencing git commit hashes vs descriptions and their tradeoffs.

## Every ID is a generated string (e.g. Unity GUID)
This approach has some benefits:
1. For Unity files this is built-in and can be reused (i.e. just read the Unity guid of that object)
2. Shorter guids can be used in some cases (like small games). For example `923a1a0c` (4 billion permutations) instead of `923a1a0c-bfff-4eec-b567-f3727571edc8` (many permutations). Your mileage may vary because this disregards hash collisions (which really should not be disregarded).

It also has some drawbacks:
1. Names are not closely connected to their values and require extra context/lookups to connect them mentally as a reader.
2. GUIDS can change sometimes for unclear reasons. This is especially important if your GUIDS are-the-same-as or mirror the guids of the Unity files, e.g. ScriptableObjects.
3. Hash collisions can and will happen. For example in Unity - https://forum.unity.com/threads/guid-collisions-when-importing-packages.1149776/

## Every ID is in int (e.g. an enum)
This approach has some benefits:
1. Code completion (if enum)
2. Names can be closely connected to their values (if enum)

It also has some drawbacks:
1. Partial enum classes do not exist so there might be a very large enum file (e.g. 10000 entries) which could lead to merge conflicts, etc.
2. Reordering is difficult, e.g. when the enums are serialized as a number. This becomes relevant when removing elements from the middle of the list.

## Every ID is an object (pass by value)
This is a terrible idea because it has a few key disadvantages:
1. If the object in question changes all of its usages have to change (large space requirement).
2. The object is stored as-is so when IDing a scene the ID will be that scene and could be multiple MBs on disk (large space requirement).
3. It's hard to have a flat list of ID's. That list will be big because each element is big (because stored by value) which means moving individual elements will likely change large chunks of the file, possible leading to more merge conflicts.

# Conclusion
Generally, I would recommend using guid strings for Ids because enums are too difficult to manage for large projects with large teams. Specifically, I would advice to use ScriptableObjects with descriptive file names and referencing them by their guids. That's what Unity does and working agains that is a bad idea.