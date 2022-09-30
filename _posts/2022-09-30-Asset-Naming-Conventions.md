---
title: "Asset Naming Conventions"
date: 2022-02-03
---

**General Learnings**


**Double Underscores**
Some teams use double underscores (`__`) as part of a asset name.
For example `Tree_1__Large` might be used to signify that a tree is large.
This signifier is generally architecturally problematic:
- There may be mistakes in the name, eg. `_` separators instead of `__` at which point the naming convention becomes inconsistent which makes it less helpful for organization.
- 