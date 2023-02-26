---
title: "Structs and Classes in Unity"
date: 2023-02-06
---

## Introduction
Which should you use ti make your Unity game - classes or structs?
Both.

## Reasoning
It all depends on the use case:
**Classes**
- need to derive, e.g. from a ScriptableObject or MonoBehaviour
- need to be passed by reference, e.g. some sort of controller like a PlayerController
- need to communicate with lots of other classes (thereby generally being less modular)

**Structs**
- pass by value, e.g. readonly data such as server responses
- simple data models which are small so that they can live on the stack

## Further reading

Records are only partially implemented in unity as of Unity 2021.2, see https://www.sunnyvalleystudio.com/blog/unity-csharp-9-features
They are great for modelling data, e.g. Event messages because of their built-in setters/getters, and hopefully soon they will also use constructors, which makes breaking changes more clear by causing compile errors.