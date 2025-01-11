# 🖳 My Ubuntu Setup

## Install Ubuntu

- Make a bootable drive
- Boot with the drive
- Install Ubuntu with appropriate configurations

## Update The Packages

```sh
sudo apt update
sudo apt upgrade
sudo apt install nala
```

## Update Snap Store

```sh
sudo snap refresh snap-store
```

> Uninstall snap version of Firefox browser

## Install necessary packages

```sh
sudo nala install curl wget git git-flow build-essential net-tools gnome-tweaks gnome-shell-extension-manager btop gdb ubuntu-restricted-extras vlc libgtop2-dev
```

### Install Fastfetch

```sh
sudo add-apt-repository ppa:zhangsongcui3371/fastfetch
sudo nala update
sudo nala install fastfetch
```

## Install Ghostty Terminal

```sh
source /etc/os-release
GHOSTTY_DEB_URL=$(
 curl -s https://api.github.com/repos/mkasberg/ghostty-ubuntu/releases/latest | \
 grep -oP "https://github.com/mkasberg/ghostty-ubuntu/releases/download/[^\s/]+/ghostty_[^\s/_]+_amd64_${VERSION_ID}.deb"
)
GHOSTTY_DEB_FILE=$(basename "$GHOSTTY_DEB_URL")
curl -LO "$GHOSTTY_DEB_URL"
```

> Install the .deb setup file

> Setup the config for ghostty at ~/.config/ghostty/config

## Enable Ubuntu Pro

```sh
sudo pro attach HwtRJPaT6huyLd2CUzcJ1u4XuC13BX
```

## Setup Zsh and Oh My Zsh

1. Install Zsh

   ```sh
   sudo nala install zsh
   chsh -s $(which zsh)
   ```

   > Restart terminal

2. Setup Oh My Zsh

   ```sh
   sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
   ```

3. Add zsh-sytax-highlighting plugin

   ```sh
   git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
   ```

   > Add zsh-syntax-highlighting in plugins list in .zshrc file

4. Install Powerlevel10k theme for OhMyZsh

   > Install Nerd Font for symbols e.g. JetBrainsMono Nerd Font

   ```sh
   git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
   ```

   > change theme to powerlevel10k/powerlevel10k in .zshrc file

## Setup Ubuntu's look and feel

> NOTE: My personal configurations

1. Tweak system settings

2. Install fonts such as JetBrainsMono Nerd Font and Nepali fonts

3. Gnome extensions
   - Appindicator and KStausNotifierItem Support - [ 3v1n0 ] (Disable System Appindicator First)
   - Apps Menu - [ fmuellner ]
   - Blur my Shell - [ aunetx ]
     - Default pipeline - NGB { R: 0, B: 1 }
     - Overview pipeline - NGB { R: 40, B: 0.2 }
     - Panel - Static, Default, Disable in overview
     - Overview - Overview, Transparent, Sigma: 100, B: 0.6, Folder: Transparent
     - Dash - Off
     - Application - Off
     - Other - LSB(Overview pipeline), SCB (Overview pipeline), Alt-Tab (Default pipeline)
   - Clipboard Indicator - [ Tudmotu ]
   - Logo Menu - [ Aryan Kausik ]
   - Extension Manager - Software Center: snap-store
   - Places Status Indicator - [ fmuellner ]
   - [QSTweak] Quick Setting Tweaker - [ qwreey ] - Mostly options on except JS Regex
   - System Monitor - [ fmuellner ]
   - Ubuntu Dock
     - Icon Size: 32
     - Behaviour - { CA: Focus, minimize or show preview, SA: Cycle through windows }
     - Appearance - { Indicator: Dots (Dominant color), Dynamic: 0 to 100 }

## Setup Flatpak (Optional)

```sh
sudo add-apt-repository ppa:flatpak/stable
sudo nala update
sudo nala install flatpak
sudo nala install gnome-software-plugin-flatpak
flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
```

## Install Web Browsers

1. For Brave browser

   ```sh
   curl -fsS https://dl.brave.com/install.sh | sh
   ```

   - Setup Brave browser
   - Import Bookmarks
   - Extensions
     - Color Picker - Eyedropper Tool
     - CSS Peeper
     - Dark Reader
     - GoFullPage - Full Page Screen Capture
     - JSON Formatter
     - React Developer Tools
     - VisBug
     - Wappalyzer
     - WhatFont

2. For Zen browser (Optional)

   > NOTE: Flatpak is needed to download Zen browser

   ```sh
   flatpak install flathub io.github.zen_browser.zen
   ```

   - Setup Zen browser
   - Import Bookmarks
   - Extensions

     - JSON Formatter
     - Disable default by about:config
     - Dark Reader
     - React Developer Tools
     - VisBug
     - Wappalyzer
     - WhatFont
     - uBlock Origin

   - Sign in to Mozilla Firefox Account (Optional)

## Login to Gnome with Google account

## Install other GUI apps

- Spotify Music Player

  ```sh
  curl -sS https://download.spotify.com/debian/pubkey_C85668DF69375001.gpg | sudo gpg --dearmor --yes -o /etc/apt/trusted.gpg.d/spotify.gpg
  echo "deb http://repository.spotify.com stable non-free" | sudo tee /etc/apt/sources.list.d/spotify.list
  sudo nala update
  sudo nala install spotify-client
  ```

- OBS Studio

  ```sh
  sudo add-apt-repository ppa:obsproject/obs-studio
  sudo nala update
  sudo nala install ffmpeg obs-studio
  ```

## Install development tools

- VS Code

  > NOTE: This command downloads the specified version of VS Code

  ```sh
  wget https://vscode.download.prss.microsoft.com/dbazure/download/stable/fabdb6a30b49f79a7aba0f2ad9df9b399473380f/code_1.96.2-1734607745_amd64.deb
  ```

  > Install the .deb setup file

  > Login to GitHub account and setup VS Code

- Tmux

  ```sh
  sudo nala install tmux
  git clone https://github.com/tmux-plugins/tpm ~/.config/tmux/plugins/tpm
  ```

  > Setup the config for tmux at ~/.config/tmux/tmux.config

- Neovim

  ```sh
  sudo add-apt-repository ppa:neovim-ppa/unstable -y
  sudo nala update
  sudo nala install make gcc ripgrep unzip git xclip neovim
  git clone https://github.com/nvim-lua/kickstart.nvim.git "${XDG_CONFIG_HOME:-$HOME/.config}"/nvim
  ```

  > Start Neovim

  > Setup the config for neovim at ~/.config/nvim
  >
  > `Enable neotree, webdevicons, tabstop = 2, shiftwidth = 2, lsp (clangd, html_ls, css_ls, ts_ls, pyright)`

- NodeJS

  ```BASH
  curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
  nvm install --lts
  ```

- DenoJS

  ```sh
  curl -fsSL https://deno.land/install.sh | sh
  ```

- PNPM

  ```sh
  curl -fsSL https://get.pnpm.io/install.sh | sh -
  ```
