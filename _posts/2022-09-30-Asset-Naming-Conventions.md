---
title: "Asset Naming Conventions"
date: 2022-02-03
---

## Consistency

**Language consistency**

It is important for teams to use a single language when naming assets because this reduces (to one) the number of possible languages that will need to be searched for when looking for an asset. For example, if this is not the case and there are two languages an artist will not know whether to look for "Baum" (German) or "Tree" (English) which means it takes longer to find what you are looking for.

**Consistency within domains**
Not all files in a Unity project need to follow the same conventions, here are some examples:
- C# files might use PascalCasing
- JSON loca files might use kebab-casing 

However:
- All C# files should have consistent rules for casing. [Microsoft Code Conventions is a good place to start](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/coding-style/coding-conventions).
- Particularly all JSON files should have consistent naming because these files will probably be searched a lot and generally won't have auto-complete and linting (like C# normally has nowadays through tools like JetBrains Rider)


**Double Underscores**
Some teams use double underscores (`__`) as part of a asset name.
For example `Tree_1__Large` might be used to signify that a tree is large.
This signifier is generally architecturally problematic:
- There may be mistakes in the name, eg. `_` separators instead of `__` at which point the naming convention becomes inconsistent which makes it less helpful for organization.
