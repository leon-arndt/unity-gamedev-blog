---
title: "Measuring Developer Productivity"
date: 2022-02-03
---

## Disclaimer
First and foremost we should measure ourselves against our past self. For example, ask yourself questions like "have I opened more PRs this year or last year?" At the end of the day productivity is hard to measure and it may be more helpful to simply identify problems wih your approach and work on those than to try and increase artificial metrics.
In general, productivity will always be hard to measure because many soft-skills such as communication may also be an important skill to practice as a developer.

Measuring developer productivity is important in teams to determine who should earn rewards (such as a bonus) and who needs to improve on their skills.
I have used different systems over time and I will cover their strengths and weaknesses.

## My Journey
### 2012: Lines of Code

When I was a teenager I felt very productive when writing a lot of code.
This lead to funny situations where I would purposefully avoid writing reusable functions in order to achieve more lines of code.
This lead to a codebase with more code which meant that other developers on the team would need to read/understand more code in order to work with the codebase. This also meant that changing a design would require manually changing code in many places.

### 2020: Number of Commits

In 2020 I though that number of commits would be a good way to measure developer performance.
One weakness of this technique is that its meaningfulnes is arbritary and could vary between equally competent and productive developers.
Imagine that one developer only commits when they have solved the task while a second developer commits after every line of code changed.
Both solved the same problem but one of them will have many more commits.

### 2022: Pull requests and Knowledge
This metric can be split into two parts:
1. Number of PR opened
2. Number of lines of knowledge generated

Performance = 10 * Number of PR opened + Number of lines of knowledge generated
... or something along those lines.
Number of PRs opened solves the problem with number of commits. Even if two developers use a different number of commits to solve a problem, they will both open 1 PR for it.

Knowledge:
Generally, it is helpful to have developers who know things about the project. This knowledge will help them to make better decisions.
However, knowledge is hard to quantify. The system I use for myself is a sort of engineering daybook where I split my work into 1) specific workday files and 2) specific work tasks (such as Jira issues). This notebook is digital, while I use small scribbles with pen and paper I have noticed that it is much more comfortable to lookup notes on a year-old Jira ticket in a digital file system instead of searching through real-life paper.

This idea is similar to the Engineering Daybooks presented in the [Pragmatic Programmer](https://www.oreilly.com/library/view/the-pragmatic-programmer/9780135956977/f_0041.xhtml).


To quantify knowledge I count the total number of lines in the relevant subfolder of my engineering daybook. This simple number can then be studied check metrics such as lines-of-knowledge generated each month, highest-performing days of the week, etc. These metrics can be studied using git commits or by taking manual snapshots; for example by using automated bash scripts which count lines of code with tools such as [cloc](https://github.com/AlDanial/cloc).
