# homelab-linux
Ansible playbook that is used for setting up host for k3s

## Base

Fedora Server 43 with / (15GB), /var (50GB) and /home (5GB) filesystems on
small intel PC with 16GB memory and 256GB.

## Preliminary steps

- setup ssh keys for GitHub access
- `dnf install ansible ansible-lint git`

## Ansible Playbook

- fix hostname from localhost
- atuin, figlet, neovim and zsh as present packages
- deny root login with password in ssh

## Tips & Tricks

- when spinning off filesystems from root, use `rsync -aX` instead of just `rsync -a` to get all fs attributes transferred as well.
- once new filesystem is mounted run `restorecon -RFv /var` for SELinux
