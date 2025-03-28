[Go Back](https://rmelendez.net)


- When building *Plasma Applets* from *Source* make sure to have the following dependencies installed
	-  `sudo pacman -S cmake extra-cmake-modules`
- For *Plasma Thermal Monitor* [GitLab Repo](https://gitlab.com/agurenko/plasma-applet-thermal-monitor/-/tree/master) make sure to installe **1.1 Dependencies**

## Tiling 
[Krohnkite](https://github.com/anametologin/krohnkite) - A dynamic tiling extension for KWin
- *Note: this is one of the best Tiling Options in KDE at the moment 10/2/24*
- [Klassy](https://github.com/anametologin/krohnkite) - Klassy is a highly customizable binary Window Decoration, Application Style and Global Theme plugin for recent version of the KDE Plasma desktop, *Note: this works really well with Krohnkite reason why this is under it*
## Panel Widget & Configuration
**Presentation Mode** - KDE Built in option to prevent display to go to sleep/suspend, to enable:
1. Add display configuration panel widget
2. Click on the added widget and the "Presentation mode option" will pop up
3. Enable as needed, just don't leave it on all the time

**Keybinds**
*Note: For Meta+D to work you need to create a new `command or script` shortcut and add the following*
`pgrep wofi >/dev/null 2>&1 && killall wofi || wofi --show drun`

| Input        | Output                         |
| ------------ | ------------------------------ |
| Meta+Q       | Close Window                   |
| Meta+J       | Krohnkite: Focus Down          |
| Meta+H       | Krohnkite: Focus Left          |
| Meta+L       | Krohnkite: Focus Right         |
| Meta+K       | Krohnkite: Focus Up            |
| Meta+Shift+> | Move Window to Next Screen     |
| Meta+Shift+< | Move Window to Previous Screen |
| Meta+,       | Krohnkite:                     |
| Meta+F       | Make Window Fullscreen         |
| Meta+D       | Open Wofi/Closes it            |

**KDE Reused Keybinds**

| **Input**        | **Output**                     | New               |
| ---------------- | ------------------------------ | ----------------- |
| Meta + T         | Toggle Tiles Editor            | Unassiged 3/2025  |
| Meta             | Activate Application Launcher  | Alt               |
| Meta+Q           | Show Activity Switcher         | Unassigned 3/2025 |
| Meta+L           | Lock Session                   | Meta+Shift+P      |
| Meta+Shift+Right | Move Window to Next Screen     | Meta+Shift+>      |
| Meta+Shift+Left  | Move Window to Previous Screen | Meta+Shift+<      |
| Meta+D           | Peek at Desktop                | Unassigned 3/2025 |
|                  |                                |                   |


