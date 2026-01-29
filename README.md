# 0x00webs Configs

This repository contains my **personal configuration files** for daily development.
It’s organized to help me quickly set up a new machine or maintain a consistent environment across systems.

### Structure

```
.
├── git/              # Git configuration files
│   └── .gitconfig
├── ssh/              # SSH keys and config
│   ├── config
│   └── README.md
├── vscode/           # Visual Studio Code settings
│   ├── settings.json
│   └── README.md
└── README.md         # This file
```

### Overview

* **git/** – My `.gitconfig` for aliases, commit helpers, color settings, merge/diff tools, and multi-account support.
* **ssh/** – SSH configuration and documentation, including aliases for GitHub and other hosts.
* **vscode/** – Custom VSCode settings for an optimized workflow.

### Usage

1. **Git** – Copy or include `.gitconfig` into `~/.gitconfig`:

   ```bash
   cp git/.gitconfig ~/.gitconfig
   ```
2. **SSH** – Copy the config to `~/.ssh/config` and set correct permissions:

   ```bash
   cp ssh/config ~/.ssh/config
   chmod 600 ~/.ssh/config
   ```
3. **VSCode** – Copy `settings.json` to your VSCode user settings folder:

   ```bash
   cp vscode/settings.json ~/.config/Code/User/settings.json
   ```

> Each directory contains its own README for more detailed setup instructions.

---

### TL;DR

This repository is my **go-to toolkit** for quickly setting up development environments with consistent **Git, SSH, and VSCode configurations**.
