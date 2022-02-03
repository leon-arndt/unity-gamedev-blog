---
title: "Side Effects In Unity"
date: 2022-02-03
---

# Side Effects In Unity
Can be helpful in avoiding bugs and making your code more readable, especially in large teams where the codebase can be huge.

```C#
if (ShowTheUiScreen()) PauseGame();
```

bool ShowTheUiScreen().
Here the response from ShowTheUiScreen is unclear, why is this returning a bool? Because the returned value is not named its usage is unclear.

It may be better to written by assigning a local variable which has an extension property which can be used to determine whether the game should be paused.

```C#
var screen = ScreenType.PauseScreen;
var ui = ShowTheUiScreen(screen):
if (ui.ShouldPauseGame) {
PauseGame();
}
```
This also allows for multiple pieces of info about the UI to be used to change the behaviour without making the UI display method more complex (which allows for better Single-responsibility principle)
```C#
var screen = ScreenType.PauseScreen;
var ui = ShowTheUiScreen(screen):
if (ui.ShouldPauseGame) {
PauseGame();
}
if (ui.ShouldPlayOpenSound) {
PlayOpenSound();
}
```

If you find yourself copy-pasting this code a lot, it might make sense to split it into categories, such as a screen category

```C#
void ShowScreen(MajorScreenType type) {
var screen = ScreenType.PauseScreen;
var ui = ShowTheUiScreen(type):
PauseGame();
PlayOpenSound();
}

```


That's it.