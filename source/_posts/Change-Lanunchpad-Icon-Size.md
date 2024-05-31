---
title: Change Lanunchpad Icon Size
date: 2019-05-10 14:35:18
tags: [Mac]
---

**How to Adjust the Icon Grid Count of Launchpad in Mac OS X**

replacing the `X` numbers for the appropriate columns and grid icon counts

``` bash
defaults write com.apple.dock springboard-columns -int X;defaults write com.apple.dock springboard-rows -int X;defaults write com.apple.dock ResetLaunchPad -bool TRUE;killall Dock
```

For example, to set the Launchpad grid to `8 × 7` you’d use the following syntax:

``` bash
defaults write com.apple.dock springboard-columns -int 7;defaults write com.apple.dock springboard-rows -int 8;defaults write com.apple.dock ResetLaunchPad -bool TRUE;killall Dock
```

If you want to return to the default setting, just change the column and row counts back to what yours was originally. **The default on my MacBook Pro Retina display is a 5 x 7 grid**, but yours may be different depending on screen size and screen resolution.

``` bash
defaults write com.apple.dock springboard-columns -int 7;defaults write com.apple.dock springboard-rows -int 5;defaults write com.apple.dock ResetLaunchPad -bool TRUE;killall Dock
```

---

**The commands** for customizing the Launchpad layout **can also be split apart** if desired like so:

**Set the Launchpad Column Icon Count**

``` bash
defaults write com.apple.dock springboard-columns -int 7
```

**Set the Launchpad Row App Icon Count**

``` bash
defaults write com.apple.dock springboard-rows -int 8
```

**Reset Launchpad**

``` bash
defaults write com.apple.dock ResetLaunchPad -bool TRUE;
```

**Relaunch the Dock with killall**

``` bash
killall Dock
```

You can also choose to just set a custom row or just a custom column count, but you must **reset and refresh the Launchpad**, and finally killall Dock to relaunch the Dock in Mac OS X and have the changes to take effect regardless of how you customize it.
