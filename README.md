# Alfred Workflows

A collection of personal [Alfred 3](https://www.alfredapp.com/) workflows that help me in my daily life and may help you too.

## [Amphetamine Switcher](https://github.com/AlessandroAime/AlfredWorkflows/raw/master/AmphetamineSwitcher.alfredworkflow)

*Requires [Amphetamine](https://itunes.apple.com/us/app/amphetamine/id937984704?mt=12), a little free app that lives in your menu bar. It gives you a graphical user interface for the caffeinate command line utility built into every Mac. With Amphetamine, you can easily and quickly override your energy saver settings and keep your Mac awake, without even lifting your fingers from the keyboard.*

With this workflow you can easily start and end Amphetamine sessions within a second. If a session is already running, it will be ended. Otherwise, a new endless session will be started.

``` applescript
tell application "System Events"
	keystroke "X" using {command down, shift down}
end tell
```

You have to set it with your hotkeys combo (mine is ⇧+⌘+X).

I kept the keyword as `caffeine` cause this workflow is a natural adaptation from my previous usage of Caffeine, but you can change it with the one you prefer.

## [Battery Time](https://github.com/AlessandroAime/AlfredWorkflows/raw/master/BatteryTime.alfredworkflow)

*Since the macOS Sierra 10.12.2 update, we're no longer able to get the battery life time from the menubar. Altough it's still accessible in the Activity Monitor app, I find this solution tricky and no enough time-efficient.*

*Probably my best Alfred workflow as today (2017/04/09).*

This workflow helps you to see instantly the remainig battery life time. It is based on the `pmset -g batt`command, and can tell you wether the battery is charging or not, the remaining charging/discharging time and more.

I took advance of the Large Type option available in Alfred, which I believe is an underrated feature by most people. You may read more about it in the [dedicated article](https://alessandroaime.github.io/macos-sierra-battery-time-indicator-solution/) I wrote on my blog.

![Battery Time Animation](https://alessandroaime.github.io/images/battery-animation.gif)

Although the `time` keyword, I also included an ⇧+⌘+B hotkeys feature to make the call even faster.

## [Bluetooth Switcher](https://github.com/AlessandroAime/AlfredWorkflows/raw/master/BluetoothSwitcher.alfredworkflow)

Part of my list of useful switchers. This one works with the `blueutil status` command utility, and turns ON or OFF the bluetooth based on its current status.

``` bash
if [[ $(./blueutil status) == 'Status: on' ]]
then
	./blueutil off
else
	./blueutil on
fi
```

The keyword is `bluetooth`, but you can change it with the one you prefer.

## [CleanMyMac Actions](https://github.com/AlessandroAime/AlfredWorkflows/raw/master/CleanMyMac.alfredworkflow)

*Requires [CleanMyMac](http://macpaw.com/cleanmymac), an app that clean, optimize, and maintain your Mac. It scans every inch of your system, removes gigabytes of junk in just two clicks, and monitors the health of your Mac.*

Uninstalling apps and cleaning the Mac from junk files haesn't been so easy. I just have to call the trigger I want, and CleanMyMac does the job for me. 

``` applescript
tell application "CleanMyMac"
	activate
end tell
tell application "System Events"
	tell process "CleanMyMac"
		keystroke return
	end tell
end tell
```

``` bash
open -a CleanMyMac.app {query}
```

The keyword are respectively `clean` and `uninstall` (plus the name of app you want get rid of), but you can change them with the ones you prefer.

## [Countdown](https://github.com/AlessandroAime/AlfredWorkflows/raw/master/Countdown.alfredworkflow)

*I've never find myself a Pomodoro technique student, but I felt the need of a timer from time to time. I strived to find an app that let me interact through Alfred, so I came up with a built-in countdown workflow.*

The behaviour of this workflow is really simple: you call it with `timer` plus the minutes you countdown should run. At the end of it you'll get a `Take a break` Large Type with a sweet alarm.

This workflow has been designed for scenarios where I'm really into something that I forget to take breaks. That's why I kept it really simple, so you won't be able too see how much time is missing to the end.

## [Files Visibility](https://github.com/AlessandroAime/AlfredWorkflows/raw/master/FilesVisibility.alfredworkflow)

This workflow helps you change the files visibility in a click, wheter you need to `show` hidden files, or `hide` them.

``` bash
defaults write com.apple.finder AppleShowAllFiles ON
killall Finder
```

``` bash
defaults write com.apple.finder AppleShowAllFiles OFF
killall Finder
```

## [Force Empty Trash](https://github.com/AlessandroAime/AlfredWorkflows/raw/master/ForceEmptyTrash.alfredworkflow)

When your Trash is moody and some files are stuck in it, you can force it to get rid of those junkies by typing `force` (or whatsoever word you think it is more appropriate).

``` bash
rm -rf ~/.Trash/*
```

## [Kill Application](https://github.com/AlessandroAime/AlfredWorkflows/raw/master/KillApplication.alfredworkflow)

Sometimes can happen that an app stops working. This workflow is the simplest incarnation of the `killall` command utility: just call it via `kill` plus the app/process you want to kill, and let your computer do the dirty job.

``` bash
killall {query}
```

## [RAM Disk](https://github.com/AlessandroAime/AlfredWorkflows/raw/master/RAMDisk.alfredworkflow)

*This is a feature I never really used, but I felt the need to build a workflow for too.*

This workflow creates a 1 GB RAM Disk, but you can easily improve it by asking a numerical argument, which will be the GB size of your disk.

``` bash
diskutil erasevolume HFS+ 'RAM Disk' `hdiutil attach -nomount ram://2097152`
```

The heyword is `ram`, but you can change it with the one you prefer.

## [Screen Recorder](https://github.com/AlessandroAime/AlfredWorkflows/raw/master/ScreenRecorder.alfredworkflow)

*Even tough QuickTime Player is hardly used on a daily basis, it still have unique built-in features such as recording an iPhone/iPad screen while it's attached via USB or simply recording the Mac screen, and so forth.*

This workflow lets you easily record your Mac screen with QuickTime Player. Pretty straight forward.


``` applescript
tell application "QuickTime Player" to activate
tell application "System Events" to tell process "QuickTime Player"
	keystroke "n" using {command down, control down}
	delay 1
	keystroke space
end tell
```

The keyword is `record`, but you can change it with the one you prefer.

## [WiFi Switcher](https://github.com/AlessandroAime/AlfredWorkflows/raw/master/WiFiSwitcher.alfredworkflow)

Last but not least, the WiFi switcher. It works with the `networksetup` command utility, and turns ON or OFF the WiFi interface based on its current status.

``` bash
interface="en1"
ret=`networksetup -getairportpower $interface`
if [[ "$ret" == *On* ]]
then
	networksetup -setairportpower $interface off
else
	networksetup -setairportpower $interface on
fi
```

The keyword is `wifi`, but you can change it with the one you prefer.
