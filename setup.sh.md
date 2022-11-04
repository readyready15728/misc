# setup.sh
## Making a new installation comfy quickly

Scuffed Ansible until I start learning the real thing, intended for CLI-based Debian systems (systems being run with GUI will need some alterations with Vim compilation and JDK version):

```bash
#!/bin/bash

USER=readyready15728

## Useful for preventing 404; also I want to upgrade whatever can be
sudo apt update
sudo apt upgrade

## Needed prerequisite packages
sudo apt install fish git fortune-mod fortunes-bofh-excuses fortunes-de fortunes-debian-hints fortunes-off fortunes-spam fortunes-ubuntu-server

## Change default shell to fish and configure fish
sudo chsh -s /usr/bin/fish $USER
# The below screws up the terminal for some reason
# curl -L https://get.oh-my.fish | fish
mkdir -p ~/.config/fish
cat << EOF >> ~/.config/fish/config.fish
status --is-interactive; and begin
  echo
  fortune
  echo
end
EOF

## Compilation and installation of Vim
mkdir ~/src
cd ~/src
git clone https://github.com/vim/vim
cd vim
# The following is adapted from https://github.com/Valloric/YouCompleteMe/wiki/Building-Vim-from-source and may need alteration
sudo apt install build-essential libncurses-dev python3-dev
# Change this to suit taste
./configure --enable-python3interp=yes --enable-terminal --enable-multibyte
make
sudo make install

## Configuration of Vim
mkdir -p ~/programming/misc
cd ~/programming/misc
git clone https://github.com/readyready15728/dot-vimrc
cd
ln -s ~/programming/misc/dot-vimrc/.vimrc
mkdir ~/.vim
cd ~/.vim
ln -s ~/programming/misc/dot-vimrc/vundle.vim
cd
git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
vim -c 'PluginInstall' -c 'qa'
cd ~/.vim/bundle/YouCompleteMe
sudo apt install cmake npm golang openjdk-20-jdk-headless
python3 install.py --all

## Install trash-cli
sudo apt install trash-cli

## Install OCaml and important ecosystem tools
bash -c "sh <(curl -fsSL https://raw.githubusercontent.com/ocaml/opam/master/shell/install.sh)"
opam init
opam update
eval $(opam env)
opam install -y async core js_of_ocaml js_of_ocaml-ppx merlin utop ocp-indent
cat << EOF >> ~/.config/fish/config.fish

eval (opam env)
EOF

## Remind user to install oh-my-fish
echo
echo "DON'T FORGET TO INSTALL oh-my-fish!!!"
```
