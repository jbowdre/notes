---
tags:
  - linux
  - nix
---
*Specifically for use with [my Nix dotfiles](https://github.com/jbowdre/dotfiles)*

```
# clone dotfiles
git clone https://github.com/jbowdre/dotfiles.git ~/.dotfiles

# install nix (single-user)
sh <(curl -L https://nixos.org/nix/install) --no-daemon

# install home-manager
nix-channel --add https://github.com/nix-community/home-manager/archive/master.tar.gz home-manager
nix-channel --update
nix-shell '<home-manager>' -A install

# activate magic
cd ~/.dotfiles
home-manager switch -b backup --flake .#$USER@$(hostname -s) \
--extra-experimental-features nix-command \
--extra-experimental-features flakes

# switch to fish
echo "$(which fish)" | sudo tee -a /etc/shells
chsh -s $(which fish)

# reload config as necessary
switch-home
```
