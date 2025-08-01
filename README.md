# 💻 My Ubuntu Setup

## Install Ubuntu

- Make a bootable drive
- Boot with the drive
- Install Ubuntu with appropriate configurations

## Update The Packages

```sh
# Update packages
sudo apt update
sudo apt upgrade
sudo apt install nala git
sudo nala full-upgrade
```

## Update Snap Store

```sh
# Update Snap Store
sudo snap refresh snap-store
```

> Uninstall snap version of Firefox browser

## Install necessary packages

```sh
# Install essential packages
sudo nala install curl wget git git-flow build-essential net-tools gnome-tweaks gnome-shell-extension-manager btop gdb ubuntu-restricted-extras vlc libgtop2-dev fzf ripgrep tldr bat
```

### Install Fastfetch

```sh
# Install fastfetch
sudo add-apt-repository ppa:zhangsongcui3371/fastfetch
sudo nala update
sudo nala install fastfetch
```

## Install Ghostty Terminal

```sh
# Download Ghostty terminal
source /etc/os-release
GHOSTTY_DEB_URL=$(curl -s https://api.github.com/repos/mkasberg/ghostty-ubuntu/releases/latest | grep -oP "https://github.com/mkasberg/ghostty-ubuntu/releases/download/[^\s/]+/ghostty_[^\s/_]+_amd64_${VERSION_ID}.deb")
GHOSTTY_DEB_FILE=$(basename "$GHOSTTY_DEB_URL")
curl -LO "$GHOSTTY_DEB_URL"
```

> Install the .deb setup file

> Setup the config for ghostty at ~/.config/ghostty/config

## Setup Zsh and Oh My Zsh

1. Install Zsh

   ```sh
   # Install zsh
   sudo nala install zsh
   ```

   > Restart terminal

2. Setup Oh My Zsh

   ```sh
   # Setup Oh My Zsh
   sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
   ```

3. Add zsh-sytax-highlighting plugin

   ```sh
   # Install syntax highlighting plugin
   git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
   ```

   > Add zsh-syntax-highlighting in plugins list in .zshrc file

4. Install Powerlevel10k theme for OhMyZsh

   > Install Liga SFMono Nerd Font (Current)

   ```sh
   # Install powerlevel10k theme
   git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
   ```

   > change theme to powerlevel10k/powerlevel10k in .zshrc file

## Setup Ubuntu's look and feel

> NOTE: My personal configurations

1. Tweak system settings and configure I/O sound using `alsamixer`

2. Gnome extensions
   - Appindicator and KStausNotifierItem Support - [ 3v1n0 ] (Disable System Appindicator First)
   - Apps Menu - [ fmuellner ]
   - Blur my Shell - [ aunetx ]
     - Default pipeline - NGB { R: 0, B: 1 }
     - Overview pipeline - NGB { R: 40, B: 0.2 }
     - Transparent pipeline - No Effects
     - Panel - Static, Transparent, Disable in overview
     - Overview - Overview, Transparent, Sigma: 100, B: 0.6, Folder: Transparent
     - Dash - Off
     - Application - Off
     - Other - LSB(Overview pipeline), SCB (Overview pipeline), Alt-Tab (Default pipeline)
   - Clipboard Indicator - [ Tudmotu ]
   - Logo Menu - [ Aryan Kausik ]
     - Extension Manager
     - Software Center: snap-store
   - Places Status Indicator - [ fmuellner ]
   - [QSTweak] Quick Setting Tweaker - [ qwreey ] - Mostly options on except JS Regex
   - System Monitor - [ fmuellner ]
   - Ubuntu Dock
     - Icon Size: 32
     - Behaviour - { CA: Focus, minimize or show preview, SA: Cycle through windows }
     - Appearance - { Indicator: Dots (Dominant color), Dynamic: 0 to 100 }

## Install Web Browser

- Brave browser (Chromium based)

  ```sh
  # Install Brave browser
  curl -fsS https://dl.brave.com/install.sh | sh
  ```

  - Setup Brave browser
  - Import Bookmarks
  - Extensions
    - Dark Reader
    - JSON Formatter [Dark: Icecoder, Light: Eclipse]
    - React Developer Tools
    - Redux DevTools
    - Wappalyzer
    - WhatFont
    - Material Icons for GitHub

- Zen browser (Firefox based) [Optional]

  - Install Zen browser using tarball script

    ```sh
    bash <(curl -s https://updates.zen-browser.app/install.sh)
    ```

  - Create a `zen-local` file inside `/etc/apparmor.d` directory with the following content if a warning pop us when starting up the browser

    ```sh
    # This profile allows everything and only exists to give the
    # application a name instead of having the label "unconfined"
    abi <abi/4.0>,
    include <tunables/global>
    profile zen-local
    /home/{username}/.tarball-installations/zen/{zen,zen-bin,updater}
    flags=(unconfined) {
      userns,
      # Site-specific additions and overrides. See local/README for details.
      include if exists <local/zen>
    }
    ```

    **NOTE:** Replace {username} with your username, There will also some configurations needed to be done after initial startup.

  - Extensions

    - Zen Mods

      - Floating status bar
      - Smaller compact mode

    - uBlock Origin
    - Dark Reader
    - Material Icons for GitHub
    - WhatFont
    - JSON Formatter
    - Wappalyzer

## Install other GUI apps

- Spotify Music Player

  ```sh
  # Install Spotify
  curl -sS https://download.spotify.com/debian/pubkey_C85668DF69375001.gpg | sudo gpg --dearmor --yes -o /etc/apt/trusted.gpg.d/spotify.gpg
  echo "deb https://repository.spotify.com stable non-free" | sudo tee /etc/apt/sources.list.d/spotify.list
  sudo nala update
  sudo nala install spotify-client
  ```

- OBS Studio

  ```sh
  # Install OBS Studio
  sudo add-apt-repository ppa:obsproject/obs-studio
  sudo nala update
  sudo nala install ffmpeg obs-studio
  ```

## Install development tools

- Setup Git and GitHub

  - Git config

    ```bash
    git config --global user.name "Your Name"
    ```

    ```bash
    git config --global user.email "Your Email"
    ```

    ```bash
    git config --global init.defaultBranch "main"
    ```

  - Setup SSH key

    ```bash
    ssh-keygen
    ```

    > Copy the public key from `.ssh/` directory

    > Go to GitHub > Settings > SSH and GPG Keys then add the generated SSH key

    > Check the connection by `ssh -T git@github`

- VS Code

  > Download and install the .deb setup file

  > Login to GitHub account and setup VS Code

- Tmux

  ```sh
  # Install Tmux
  sudo nala install tmux
  git clone https://github.com/tmux-plugins/tpm ~/.config/tmux/plugins/tpm
  ```

  > Setup the config for tmux at ~/.config/tmux/tmux.config

- Neovim [Optional]

  ```sh
  # Install Neovim
  sudo add-apt-repository ppa:neovim-ppa/unstable -y
  sudo nala update
  sudo nala install make gcc ripgrep unzip git xclip neovim
  git clone https://github.com/nvim-lua/kickstart.nvim.git "${XDG_CONFIG_HOME:-$HOME/.config}"/nvim
  ```

  > Start Neovim

  > Setup the config for neovim at ~/.config/nvim

  > `Enable neo-tree, nerdfont, tabstop = 2, shiftwidth = 2, lsp`

- NodeJS

  ```BASH
  # Install NodeJS [Recommended to visit the official Node.js site]
  curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
  nvm install --lts
  ```

- DenoJS (Oprional)

  ```sh
  # Install DenoJS
  curl -fsSL https://deno.land/install.sh | sh
  ```

- PNPM (Oprional)

  ```sh
  # Install PNPM
  curl -fsSL https://get.pnpm.io/install.sh | sh -
  ```

- Python

  ```sh
  sudo nala install python3-full python3-pip python3-venv
  ```

- Docker (Oprional)

  ```sh
  # Add Docker's official GPG key:
   sudo nala update
   sudo nala install ca-certificates curl
   sudo install -m 0755 -d /etc/apt/keyrings
   sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
   sudo chmod a+r /etc/apt/keyrings/docker.asc

   # Add the repository to Apt sources:
   echo \
     "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
     $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
     sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
  ```

  ```sh
  # Install packages
  sudo nala update
  sudo nala install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
  ```

  ```sh
  # Download Docker Desktop
  wget https://desktop.docker.com/linux/main/amd64/docker-desktop-amd64.deb
  ```

  > Install the .deb setup file
