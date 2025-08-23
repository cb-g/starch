# nas

## synology docker

### registry

- download archlinux image

### image

- launch

### create-container wizard

- use the selected networks: bridge
- container name: archlinux1
- enable auto-restart
- local port: 2227, container port: 22, type: TCP
- run container

### container

- details
- terminal

root@archlinux1

```bash
pacman -Sy --needed --noconfirm archlinux-keyring && pacman -Syu --noconfirm

```

```bash
pacman -S --needed --noconfirm openssh && ssh-keygen -A

```

```bash
pacman -S --needed --noconfirm sudo

useradd -m -s /bin/bash devusr && passwd devusr

install -d -m 0755 /etc/sudoers.d && printf '%s\n' '%wheel ALL=(ALL:ALL) ALL' > /etc/sudoers.d/10-wheel && chmod 0440 /etc/sudoers.d/10-wheel && visudo -cf /etc/sudoers.d/10-wheel && usermod -aG wheel devusr

printf '%s\n' '[ -t 1 ] && sudo -v && ( while sleep 60; do sudo -n true || break; done >/dev/null 2>&1 & )' >> ~/.bashrc && printf '%s\n' '[ -f ~/.bashrc ] && . ~/.bashrc' >> ~/.bash_profile && . ~/.bashrc

```

```bash
pacman -S --needed --noconfirm neovim git

echo 'export EDITOR=nvim' >> ~/.bashrc && echo 'export VISUAL=nvim' >> ~/.bashrc && . ~/.bashrc

git config --global core.editor nvim

```

### edit-container wizard

- stop container
- folder: /docker/archlinux1, mount path: /home/devusr
- restart container

### container

root@archlinux1

```bash
su - devusr

```

devusr@archlinux1

```bash
sudo sh -c 'sshd -t && (pkill -HUP sshd 2>/dev/null || /usr/sbin/sshd -e)'

```

or `exit` and directly from root@archlinux1
```bash
sshd -t && (pkill -HUP sshd 2>/dev/null || /usr/sbin/sshd -e)

```


### ssh

local-device@local-user

```zsh
ssh -p 2227 devusr@<NAS_IP>

```

devusr@archlinux1

```bash
nvim --version

```
