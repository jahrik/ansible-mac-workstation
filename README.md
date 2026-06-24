# Mac Workstation

[![CICD](https://github.com/jahrik/ansible-mac-workstation/actions/workflows/cicd.yml/badge.svg)](https://github.com/jahrik/ansible-mac-workstation/actions/workflows/cicd.yml)
[![Ansible Galaxy](https://img.shields.io/badge/ansible--galaxy-jahrik.mac__workstation-blue?logo=ansible)](https://galaxy.ansible.com/ui/standalone/roles/jahrik/mac_workstation/)

Meta-role that installs a macOS development environment by composing jahrik.* roles. macOS only.

## OS Support

macOS (all versions with Homebrew support).

## Role Variables

| Variable | Default | Description |
|---|---|---|
| `install` | `true` | Set to `false` to uninstall |
| `time_zone` | `US/Pacific` | System timezone |
| `base_packages` | `[git, jq, tree, htop, ripgrep, fd, wget]` | Homebrew formulae |
| `editor` | `nvim` | Default `$EDITOR` |
| `lang` | `en_US.UTF-8` | `$LANG` env var |
| `python_force_color` | `1` | `PY_COLORS` env var |
| `ansible_force_color` | `1` | `ANSIBLE_FORCE_COLOR` env var |

## Dependencies

| Role | CI |
|------|----|
| jahrik.ghostty | [![CI](https://github.com/jahrik/ansible-ghostty/actions/workflows/cicd.yml/badge.svg)](https://github.com/jahrik/ansible-ghostty/actions/workflows/cicd.yml) |
| jahrik.zsh | [![CI](https://github.com/jahrik/ansible-zsh/actions/workflows/cicd.yml/badge.svg)](https://github.com/jahrik/ansible-zsh/actions/workflows/cicd.yml) |
| jahrik.nvim | [![CI](https://github.com/jahrik/ansible-nvim/actions/workflows/cicd.yml/badge.svg)](https://github.com/jahrik/ansible-nvim/actions/workflows/cicd.yml) |

## Example Playbook

```yaml
- name: Configure macOS workstation
  hosts: all
  become: false
  vars:
    install: true
  roles:
    - jahrik.mac_workstation
```

## Testing

```bash
uv sync
source .venv/bin/activate
yamllint .
ansible-lint
molecule converge -s localhost
molecule verify -s localhost
```

## License

MIT
