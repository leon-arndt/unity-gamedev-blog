---
title: "Approaching Complex Problems"
date: 2022-02-03
---

This post introduces the approach I use to solve complex problems. Try it and see if it works for you, everyone works differently. I will try to illustrate the approach using a "player double jump" feature as an example.

Generally, I break every complicated issue I work on into different categories. I consider issues complicated which I know I can't solve in 1 hour or know that I don't know enough to estimate them with some degree of confidence.

These categories are gathered in a markdown file which has the name of the problem, such as "1234-player-double-jump.md" where 1234 is the Jira issue number. Adding a issue number is helpful for cases where only the number is shared and adds an easy lookup method when working with 100's of files for one project.

## 1. Problem
This is the description of the feature, the change, the bugfix, whatever. It should be as short but precise as possible, something to give an idea of where to start. The problem should answer questions such as What? Who? Where? How? Why?

**Example**

"Add a double jump feature for the player because players requested it in the last version"

## 2. Questions
Asking the right questions helps us find helpful answers. There is no right/wrong way to ask questions but questions which lead to more detailed questions can be very helpful, for example, a question like "Where are the player controls set up?" might lead us in the right direction when starting with the problem.

I generally add the answer with a note (`A:`) right next to the question and mark the point as checked off.

**Example**
- [x] Where are the player controls set up? A: they are defined in `PlayerController.cs`
- [x] Is a triple-jump planned? A: Game design says no but I should keep the code flexible in case this changes in the future

## 3. Knowledge
Consider this section an optional addition to the Questions section. I often use this to add general info like "A previous game used RigidBody(s) to create its double jump feature".

**Example**

A previous game used RigidBody(s) to create its double jump feature.
A double jump can happen as soon as 1 frame after the first jump, this could look glitchy for players.


## 4. TODO
This is a simple todo list. Spliting the todo list down into smaller tasks makes them easier to complete and sometimes helps to uncover additional tasks. I check these off as I finish them, sometimes I also delete tasks if I don't need them anymore.

**Example**
- [x] Add a force whenever the player preses the space bar
- [x] Add list of `Powerup` ScriptableObjects to the PlayerController
- [ ] Define a `DoubleJump` `PowerUp` and check that it exists before executing double jump.
- [ ] Also consider if adding an virtual `JumpExecute()` is better than checking manually

## 5. Tests
A list of tests which should be performed before the PR is merged.

Note: some developers may advise you to write tests first. That might lead you to ask why tests aren't listed earlier. Tests can only be written if the problem is clear and understood. Writing a test too early might lead to it being written twice. I write notes on what to test (whether in code or manual) whenever I think something might be important to test.

I also add a note if a test failed and why it failed. After performing all the testing I decided on in the Editor I create a target platform build (such as Android) and test there. The target platform tests may be slightly different, in the example below, the automated level-playthrough is not possible on Android so it is left out.

If the automated level-playthroughs are possible (e.g. the Unity test runner tests) then these should be preferred because they improve test consistency.

**Example**
Android Tests:
- [x] The player can single jump
- [x] The player can double jump
- [x] The player cannot triple jump
- [x] The player can collide normally with ceilings
- [ ] The automated level-playthrough tests work normally. Note: I need to fix the jumping for double-jump levels.

Android Tests:
- [x] The player can single jump
- [x] The player can double jump
- [x] The player cannot triple jump
- [x] The player can collide normally with ceilings

## 6. Pull Request
This section will cover the text for the pull request. I prepare this before opening the pull request to visualize how other members of the team might understand the problem differently than me. This section is not just about the what, but about the why.

If you are working by yourself this step is not neccessary but it will be helpful if you are planning to work in a team because it will make you practice explaining problems and seeing them from the outside perspective.

**Example:**
```
Task: Add a double jump feature for the player.
Solution: Used a rigidbody to add the jump because rigidbody could be reused from single-jump system.
```

## Beyond the steps
- generally I have found visualizing my work helps me to work much faster. For example, imagining receiving feedback on a pull request makes me much more comfortable with the process of reacting to the feedback and replying to it.
- Using [Anki](https://apps.ankiweb.net/) cards to review common troubleshooting problems (e.g. git errors) might help you to become more familiar with common problem-solving techniques.

## Disclaimer
Most of the problems I work on have between 400-2000 Words written in their markdown files. If you find your file becoming hard to manage because it is so large you might need to break your problem down into smaller problems (this is always possible, if you don't think it is then you need to work on understanding the problem better).

Feel free to adjust this process however it suits you.