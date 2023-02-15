---
title: "Top 10 Unity Pull Request Problems"
date: 2023-02-15
---

## Introduction
This list is based on my personal experience working in big and small Unity projects.

## Top Pull Request Problems
1. Inside an UI prefab a GameObject was deactivated which should have stayed activated.
2. A BOM was added to the beginning of a file
3. Line endings do not match -> use a config to sync this setting across platforms
4. A folder meta file is missing.
5. There are unused imports in C# files.
6. The import settings for an asset (e.g. a Sprite) are incorrect.
7. An unwanted change to a TMPro asset -> fix this one by moving TMPro to a different folder (search online which folder
8. Sprite added to sprite atlas but Sprite atlas not updated -> Save project and push unpushed changes.
9. Scene merge conflicts -> solve by storing data in smaller chunks, e.g. in prefabs (`Environment.prefab`, `UserInterface.prefab`) or ScriptableObjects.
10. UserEditor settings were pushed -> add this file to the .gitignore to solve thos issue.