# Linux Configuration

Personal dotfiles for an Arch Linux desktop and development environment, with a separate NixOS configuration and platform-aware Zsh settings for Linux and macOS.

## Overview

The setup includes:

- **Wayland desktop environment** with Sway, Waybar, and Kitty
- **Development tools** for Python, Node.js, Rust, and C++
- **Chinese input method** support
- **Terminal environment** with Zsh, Oh My Zsh, tmux, fzf, and zoxide
- **AI coding tools** with dedicated configuration submodules and shell aliases
- **Mirror configurations** for faster package downloads in China on Linux
- **NixOS configuration** using flakes and Home Manager, with a River desktop

## File Structure

### Configuration Directories

| Directory/File | Purpose |
| --- | --- |
| `.config/` | Desktop and application configurations ([submodule guide](.config/README.md)) |
| `flake.nix`, `flake.lock` | Nix flake inputs and the `desktop` NixOS configuration |
| `.nix/` | NixOS system, hardware, and Home Manager configuration ([guide](.nix/README.md)) |
| `.zshrc`, `.zprofile`, `.zsh/` | Shell settings, login environment, and custom completions |
| `.tmux.conf` | tmux keybindings, plugins, and session restoration settings |
| `.gitconfig` | Git settings and aliases |
| `.claude/`, `.codex/`, `.qwen/`, `.pi/`, `.dsh/` | Tool configuration submodules |
| `.sh/` | Utility scripts for video processing, subtitles, and application wrappers |
| `.newsboat/` | RSS feeds, bookmarks, and Newsboat configuration ([guide](.newsboat/README.md)) |
| `.m2/settings.xml`, `.condarc` | Maven and Conda settings |
| `.ipaper/` | iPaper profiles and settings |
| `Videos/` | Video project submodule |
| `docs/` | Git notes and Nix reference material |

### Key Configuration Files

- **`.zshrc`** - Zsh configuration with:
  - Oh My Zsh with the `robbyrussell` theme
  - Linux/macOS detection and Homebrew integration on macOS
  - Custom functions for dates, translation, and systemd user service URLs
  - fzf completion, keybindings, previews, and zoxide navigation
  - Linux-only package mirror settings and optional nvm initialization
  - AI tool aliases, per-command proxies, and optional `~/.token` loading

- **`.config/`** - Application-specific configurations:
  - Sway (Wayland compositor), Waybar (status bar), and Kitty (terminal)
  - Neovim, maintained as a nested Git submodule
  - OBS Studio, Xremap, and Surfingkeys
  - Docker Compose stacks for iread and agentsview
  - Legacy River, Hyprland, and other desktop configurations

## Key Features

### Development Environment

- **Languages**: Python 3, Node.js, Rust, C/C++
- **Node.js shell integration**: nvm when installed; Homebrew `node@24` on macOS when available
- **Editors**: Neovim, VS Code
- **Tools and integrations**: Git, GitHub CLI, Docker, kubectl, fzf, zoxide, tmux
- **Nix-managed tools**: uv, pipx, LaTeX, Typst, and Tinymist

### Shell Enhancements

- **Oh My Zsh** with plugins: git, sudo, docker, kubectl, history, colored-man-pages, fzf
- **Custom functions**:
  - `mydate` - Custom date formatting
  - `tododate` - Todo-friendly date format
  - `tozh` / `toen` - Quick translation functions
  - `sysu` - Show local URLs for enabled, running systemd user services on Linux

The translation helpers use `trans` (Translate Shell). The shell configuration expects Oh My Zsh at `~/.oh-my-zsh` and initializes zoxide on startup.

### AI Tool Integration

Shell aliases provide shortcuts for Claude Code, Codex, OpenCode, and Qwen, including proxy and alternative-provider variants. Optional provider credentials are loaded from `~/.token`; GitHub MCP authentication is read from the GitHub CLI credential store when available. Proxy aliases use local endpoints defined in `.zshrc`.

### Package Manager Mirrors

The following environment variables are set by `.zshrc` on Linux:

- **Node/npm**: npmmirror.com (`FNM_NODE_DIST_MIRROR`, `NPM_CONFIG_REGISTRY`)
- **Python/pip**: pypi.tuna.tsinghua.edu.cn (`PIP_INDEX_URL`)
- **Rust toolchain**: mirrors.ustc.edu.cn (`RUSTUP_DIST_SERVER`, `RUSTUP_UPDATE_ROOT`)

## Usage

### Fetching Submodules

Several configuration directories are separate repositories. Clone recursively to include them and nested submodules such as Neovim:

```bash
git clone --recurse-submodules https://github.com/isomoes/linux-config.git
```

For an existing checkout, run from the repository root:

```bash
git submodule update --init --recursive
```

### Applying Configuration

The repository mirrors the home-directory layout. Symlink or copy the selected dotfiles into the corresponding paths under `~`, and install the applications they configure. Adjust personal paths, Git identity, and local proxy endpoints for your machine.

### NixOS-Specific Setup

The root `flake.nix` defines an `x86_64-linux` host named `desktop`, using `nixos-unstable` and Home Manager for user `isomo`. Its desktop configuration uses River, SDDM, Fcitx5, and NVIDIA drivers.

See [.nix/README.md](.nix/README.md) for rebuild instructions. Adapt the hardware configuration and user settings before applying it to another machine; run flake commands from the repository root.

### Shell Configuration

After updating `.zshrc`, reload the configuration:

```bash
source ~/.zshrc
```

## System Information

- **OS**: Arch Linux
- **Shell**: Zsh with Oh My Zsh
- **Display Protocol**: Wayland
- **Compositor**: Sway (Arch desktop); River (NixOS configuration)
- **Status Bar / Terminal**: Waybar / Kitty (Arch desktop)
- **Input Method**: Fcitx5
- **NixOS Time Zone**: Asia/Hong_Kong
