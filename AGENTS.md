# AGENTS.md

This file provides guidance to AI coding agents when working with code in this repository.

## Role Overview

Ansible meta-role that configures a macOS development workstation. Composes jahrik.* sub-roles from Ansible Galaxy for terminal, shell, and editor setup, plus Homebrew for package management.

## Key Variables (`defaults/main.yml`)

| Variable | Default | Description |
|---|---|---|
| `install` | `true` | Set to `false` to uninstall |
| `time_zone` | `US/Pacific` | System timezone |
| `base_packages` | `[git, jq, tree, htop, ripgrep, fd, wget]` | Homebrew formulae to install |
| `editor` | `nvim` | Default editor (passed to jahrik.zsh) |
| `lang` | `en_US.UTF-8` | Locale (passed to jahrik.zsh) |

## Task Flow

`tasks/main.yml`:
1. `homebrew.yml` - Install base Homebrew packages
2. `jahrik.ghostty` - Terminal emulator
3. `jahrik.zsh` - Zsh with Powerlevel10k
4. `jahrik.nvim` - Neovim with lazy.nvim and LSP

## Dependencies (installed via `requirements.yml`)

- `jahrik.ghostty` - Ghostty terminal (depends on `jahrik.nerd_fonts`)
- `jahrik.zsh` - Zsh shell configuration
- `jahrik.nvim` - Neovim (depends on `jahrik.nerd_fonts`)

## Testing

```bash
uv sync
source .venv/bin/activate
yamllint .
ansible-lint
molecule test
```

## CI

- **Lint**: yamllint + ansible-lint
- **Release**: publishes to Ansible Galaxy on merge to `main`
