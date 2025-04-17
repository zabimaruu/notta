[Go Back](https://rmelendez.net)

# Windows Tools

## PowerShell
Updating Winget
*Note: Looks like windows comes with an old version of  `Winget` which does not work really well*
```
Add-AppxPackage -Path '[Path_to_.msixbundle]' -ForceApplicationShutdown
```
Replace `Path_to_msixbundle` with the link of the latest released on GitHub
*Note: make sure to run terminal as Administrator*

## Terminals
### Alacritty
One of the best and fastest Terminals [Installation](https://github.com/alacritty/alacritty)
*Note:* 
Config Location
- Global config can be found at *soru/dots/windows/alacritty*
- Copy config to *%APPDATA%\alacritty\alacritty.yml* create folders as neccesary or C:\Users\dashi\AppData\Roaming\alacritty

**Create WSL2 Shortcut**
- Navigate to *"C:\Program Files\Alacritty"*
- Create a new shortcut for *Alacritty.exe*
- Right Click > Properties > Target Text Box > "C:\Program Files\Alacritty\alacritty.exe" -e wsl ~
- `-e wsl ~` *these are the parameters to add at the end of Target Text Box*

## Package Managers
### Scoop
Scoop install programs you know and love, from the command line with a minimal amount of friction. > [Installation](https://scoop.sh/)

*Check website, commands and scripts might have changed*
```powershell
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser # Optional: Needed to run a remote script the first time
irm get.scoop.sh | iex
```

**Installing Fonts**
```powershell
scoop bucket add nerd-fonts
scoop install nerd-fonts/Agave-NF-Mono
```
All other fonts can be found in *scoop* main website

```
# Terminal Config & Tricks

To change *Copy/Paste* action on Windows Terminal change these commands within *Setting.json* 

This is needed when using *Neovim in WSL2* otherwise, *Visual Block* will not work as intended

```json
"action": "copy",
"singleLine": false
"keys": "ctrl+shift+c"
"command": "paste",
"keys": "ctrl+shift+v" 
```