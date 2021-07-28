# setup.sh
## Making a new installation comfy quickly

Scuffed Ansible until I start learning the real thing, intended for CLI-based Debian systems:

```bash
#!/bin/bash

USER=readyready15728

## Useful for preventing 404; also I want to upgrade whatever can be
sudo apt update
sudo apt upgrade

## Needed prerequisite packages
sudo apt install fish git fortune-mod fortunes-bofh-excuses fortunes-de fortunes-debian-hints fortunes-off fortunes-spam fortunes-ubuntu-server

## Change default shell to fish and configure fish
echo 'Changing shell to fish'
sudo chsh -s /usr/bin/fish $USER
# curl -L https://get.oh-my.fish | fish
mkdir -p ~/.config/fish
echo > ~/.config/fish/config.fish << EOF
fortune
echo
EOF

# ## Compilation and installation of Vim
# mkdir ~/src
# cd ~/src
# git clone https://github.com/vim/vim
# cd vim
# # The following is adapted from https://github.com/Valloric/YouCompleteMe/wiki/Building-Vim-from-source and may need alteration
# sudo apt install build-essential libncurses-dev python3-dev
# # Change this to suit taste
# ./configure --enable-python3interp=yes --enable-terminal --enable-multibyte
# make
# sudo make install
#
# ## Configuration of Vim
# mkdir -p ~/programming/misc
# cd ~/programming/misc
# git clone https://github.com/readyready15728/dot-vimrc
# cd
# ln -s ~/programming/misc/dot-vimrc/.vimrc
# mkdir ~/.vim
# cd ~/.vim
# ln -s ~/programming/misc/dot-vimrc/vundle.vim
# cd
# git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
# vim -c 'PluginInstall' -c 'qa'
# cd ~/.vim/bundle/YouCompleteMe
# sudo apt install cmake npm golang
# # python3 install.py --all
#
# ## Install trash-cli
# sudo apt install trash-cli
```
