# dotfiles

> Personal dotfiles collection — Zsh aliases, Git config, VS Code settings, tmux.

## Overview

This repo manages my development environment configuration across machines. It includes:

- **Zsh** — Aliases, exports, prompt theme, completions
- **Git** — Global config, aliases, ignore patterns
- **VS Code** — Settings, keybindings, snippets
- **tmux** — Status bar, key bindings, session management

## Install

Clone the repo and run the bootstrap script:

```bash
git clone https://github.com/lanzlog/dotfiles.git ~/.dotfiles
cd ~/.dotfiles
chmod +x install.sh
./install.sh
```

The script symlinks each config file to its expected location (`~/.zshrc`, `~/.gitconfig`, etc.).

### Manual steps

If you prefer to install piece by piece:

```bash
# Zsh config
ln -sf ~/.dotfiles/zsh/.zshrc ~/.zshrc
source ~/.zshrc

# Git config
ln -sf ~/.dotfiles/git/.gitconfig ~/.gitconfig

# VS Code settings (macOS)
ln -sf ~/.dotfiles/vscode/settings.json ~/Library/Application\ Support/Code/User/settings.json
# Linux:
# ln -sf ~/.dotfiles/vscode/settings.json ~/.config/Code/User/settings.json

# tmux config
ln -sf ~/.dotfiles/tmux/.tmux.conf ~/.tmux.conf
```

## Zsh Aliases

```zsh
# Navigation
alias ..="cd .."
alias ...="cd ../.."
alias ~="cd ~"

# Git shortcuts
alias gs="git status"
alias ga="git add"
alias gc="git commit"
alias gp="git push"
alias gl="git log --oneline --graph --decorate --all"

# Listing
alias ls="ls --color=auto"
alias ll="ls -la"
alias la="ls -A"

# System
alias c="clear"
alias h="history"
alias reload="source ~/.zshrc"
```

## Git Config

```ini
[user]
    name = lanzlog
    email = lanzlog@users.noreply.github.com

[alias]
    co = checkout
    br = branch
    st = status
    ci = commit
    di = diff
    lg = log --oneline --graph --decorate --all

[core]
    editor = code --wait
    autocrlf = input

[init]
    defaultBranch = main

[push]
    autoSetupRemote = true
    default = current
```

## VS Code Settings

Key settings in `vscode/settings.json`:

```json
{
  "editor.fontSize": 14,
  "editor.fontFamily": "Fira Code, JetBrains Mono, monospace",
  "editor.fontLigatures": true,
  "editor.formatOnSave": true,
  "editor.minimap.enabled": false,
  "workbench.colorTheme": "One Dark Pro",
  "workbench.iconTheme": "material-icon-theme",
  "terminal.integrated.fontSize": 13,
  "files.exclude": {
    "**/.git": true,
    "**/node_modules": true,
    "**/__pycache__": true
  }
}
```

## tmux Config

```tmux
# Use Ctrl+a as prefix instead of Ctrl+b
set -g prefix C-a
unbind C-b
bind C-a send-prefix

# Mouse support
set -g mouse on

# Start window numbering at 1
set -g base-index 1

# Split panes
bind | split-window -h
bind - split-window -v

# Reload config
bind r source-file ~/.tmux.conf \; display "Reloaded!"

# Status bar styling
set -g status-bg colour235
set -g status-fg white
set -g status-interval 5
set -g status-left "#[fg=green]#S "
set -g status-right "#[fg=yellow]%Y-%m-%d %H:%M"
```

## Structure

```
dotfiles/
├── install.sh        # Bootstrap symlink script
├── zsh/
│   └── .zshrc        # Zsh configuration and aliases
├── git/
│   ├── .gitconfig    # Git global config
│   └── .gitignore    # Global gitignore
├── vscode/
│   ├── settings.json # Editor settings
│   └── keybindings.json
└── tmux/
    └── .tmux.conf    # tmux configuration
```

## Notes

- Works on macOS and Linux.
- VS Code paths differ slightly between platforms — adjust symlink targets accordingly.
- Back up any existing dotfiles before running `install.sh`.
