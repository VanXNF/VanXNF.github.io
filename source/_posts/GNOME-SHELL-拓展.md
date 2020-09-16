---
title: GNOME SHELL 拓展
date: 2018-10-04 20:11:55
updated: 2018-10-04 20:11:55
tags: [GNOME, SHELL]
categories: Software
---

>在使用 Ubuntu 18.04 后发现了不少好用的 GNOME SHELL 拓展插件，在此做一个推荐及备份。以下插件排名不分先后。

# [system-monitor](https://extensions.gnome.org/extension/120/system-monitor/)
>Display system informations in gnome shell status bar, such as memory usage, cpu usage, network rates…

&nsbp;&nbsp;在顶栏显示系统硬件状态，十分直观。在 Ubuntu 软件商店中即可安装，可能会遇到依赖问题，会有提示，按照具体提示安装即可，我当时提示缺少 Clutter，那就安装咯：
```
sudo apt-get install gir1.2-clutter-1.0 gir1.2-clutter-gst-3.0 gir1.2-gtkclutter-1.0
```

# [Clipboard Indicator](https://extensions.gnome.org/extension/779/clipboard-indicator/)
>Clipboard Manager extension for Gnome-Shell - Adds a clipboard indicator to the top panel, and caches clipboard history.

&nbsp;&nbsp;剪贴板管理，在顶栏查看选择历史剪贴板。

# [Coverflow Alt-Tab](https://extensions.gnome.org/extension/97/coverflow-alt-tab/)
>Replacement of Alt-Tab, iterates through windows in a cover-flow manner.

# [Dash to Dock](https://extensions.gnome.org/extension/307/dash-to-dock/)
> A dock for the Gnome Shell. This extension moves the dash out of the overview transforming it in a dock for an easier launching of applications and a faster switching between windows and desktops. Side and bottom placement options are available.

&nbsp;&nbsp;取代系统 dock 栏。

# [Gnome Shell Audio Output Switcher](https://extensions.gnome.org/extension/1028/gnome-shell-audio-output-switcher/)
>Gnome-Shell Extension: Easily switch between your audio outputs from the system menu.

# [Lock Keys](https://extensions.gnome.org/extension/36/lock-keys/)
>Numlock & Capslock status on the panel.

# [Multi Monitors Add-On](https://extensions.gnome.org/extension/921/multi-monitors-add-on/)
>Add multiple monitors overview and panel for gnome-shell.

&nbsp;&nbsp;外接屏幕神器。

# [OpenWeather](https://extensions.gnome.org/extension/750/openweather/)
>Weather extension to display weather information from https://openweathermap.org/ or https://darksky.net for almost all locations in the world.
>For openweathermap.org, you can either use the extensions default-key or register at https://openweathermap.org/appid and set the appropriate switch in the preferences dialog to "off".
>For Dark Sky you have to register at https://darksky.net/dev/register and get a personal API-key.
>Since version 29 this extensions uses coordinates to store the locations and makes the names editable to support multiple weather-providers!
>If you update from versions prior to 29 to 29 or greater (with darksky.net - support) you have to recreate your locations.

# [Pixel Saver](https://extensions.gnome.org/extension/723/pixel-saver/)
>Pixel Saver is designed to save pixel by fusing activity bar and title bar in a natural way.

# [Screenshot Tool](https://extensions.gnome.org/extension/1112/screenshot-tool/)
>Conveniently create, copy, store and upload screenshots.

# [TopIcons Plus](https://extensions.gnome.org/extension/1031/topicons/)
>This extension moves legacy tray icons (bottom left of Gnome Shell) to the top panel. It is a fork from the original extension from ag with settings for icon opacity, saturation, padding, size and tray position, along with a few minor fixes and integration with the Skype integration extension.

# [User Themes](https://extensions.gnome.org/extension/19/user-themes/)
>Load shell themes from user directory.

&nbsp;&nbsp;万物之源。

# [Suspend Button](https://extensions.gnome.org/extension/826/suspend-button/)
>Allows to modify the suspend/shutdown button in the status menu.
