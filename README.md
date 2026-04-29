# homelab-linux
Ansible playbook that is used for setting up host for k3s

## Base

Fedora Server 43 with / (15GB), /var (50GB) and /home (5GB) filesystems on
small intel PC with 16GB memory and 256GB.

## Network

### CIDR ranges

- 10.42.0.0/16 # k3s pods CIDR
- 10.43.0.0/16 # k3s service CIDR

### Ports

- 80/tcp # Traefix HTTP
- 443/tcp # Traefix HTTPS
- 6443/tcp # k3s API server
- 8472/udp # Flannel VXLAN (pod-to-pod overlay)
- 10250/tcp # kubelet
- 30222/tcp # Forgejo SSH NodePort
- 51820/udp # Flannel WireGuard (not currently in use)

## Preliminary steps

- setup ssh keys for GitHub access
- `dnf install ansible ansible-lint git neovim`

## Ansible Playbook

- fix hostname from localhost
- atuin, figlet, neovim and zsh as present packages
- helm for k3s (k3s provides kubectl on its own)
- deny root login with password in ssh
- k3s requirements: kernel modules, sysctl settings, firewall settings
- k3s and setup config for root
- postgresql into k3s
- forgejo into k3s so that it uses postgresql for users etc.
- create forgejo admin and flux user into forgejo

## Tips & Tricks

- when spinning off filesystems from root, use `rsync -aX` instead of just `rsync -a` to get all fs attributes transferred as well.
- once new filesystem is mounted run `restorecon -RFv /var` for SELinux
- when creating users into forgejo
  - your admin account can't be called `admin` or it will fail
  - all usernames and e-mails have to be unique
- k3s persistent volumes are stored under /var/lib/rancher/k3s/storage/pvc-...
