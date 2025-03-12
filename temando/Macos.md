[Go Back](https://rmelendez.net)

## Awesome resources
There are many `markdown` list in Github but the following ones are the ones I have come across to still be maintained and fairly well made

- [Open Source MacOS Application](https://github.com/serhii-londar/open-source-mac-os-apps?tab=readme-ov-file#productivity) A large list of apps, several of them are no longer maintain so check the sources out
### List of app I use the most
One liner:
```bash
# Install non-cask applications
brew install eza zsh tmux ranger neovim

# Install cask applications
brew install --cask font-fantasque-sans-mono-nerd-font obsidian nextcloud firefox bitwarden cyberduck alacritty kitty moonlight alfred keepingyouawake jdownloader skim
```
- 
#### Yabai & skhd (Tilling & Keybind manager)
These two applications work with each other to mimic how a linux **Tilling Manager** would work in **MacOS**
**Installation:**
One liner:
```bash
brew install koekeishiya/formulae/yabai
brew install koekeishiya/formulae/skhd

# Run the following commands to start/restart both services
yabai --start-service
yabai --restart-service

skhd --start-service
skhd --restart-service
```

Copy **skhd & yabai** configs located in `dots/configs/MacOS/skhd_m & dots/confings/MacOS/yabai_m` to `~/.config/skhd & ~/.config/yabai`
#### Skim
Great open source PDF viewer, probably one of the best ones for MacOS