# setup.sh
## Making a new installation comfy quickly

Self-explanatory. Got a new Pi? Just opened up a new cloud account? Here ya go:

```bash
#!/bin/sh

# Useful for preventing 404
sudo apt update

sudo apt install fortune-mod

cat << 'EOF' >> ~/.bashrc

# Eternal bash history combined with preservation of history across multiple
# tabs, drawn from:
# 
# https://stackoverflow.com/questions/9457233/unlimited-bash-history
# https://unix.stackexchange.com/questions/1288/preserve-bash-history-in-multiple-terminal-windows/
export HISTFILESIZE=
export HISTSIZE=
export HISTTIMEFORMAT="[%F %T] "
export HISTFILE=~/.bash_eternal_history
PROMPT_COMMAND="history -a; history -c; history -r; $PROMPT_COMMAND"

export TERM=xterm-256color

fortune
EOF

mkdir ~/src
cd ~/src
git clone https://github.com/vim/vim
cd vim
# The following is adapted from https://github.com/Valloric/YouCompleteMe/wiki/Building-Vim-from-source and may need alteration
sudo apt install build-essential libncurses-dev libgnome2-dev libgnomeui-dev libgtk-3-dev libatk1.0-dev libbonoboui2-dev libcairo2-dev libx11-dev libxpm-dev libxt-dev python3-dev git
# Change this to suit taste
./configure --enable-gui=gtk3 --enable-python3interp=yes --enable-terminal --enable-multibyte
make
sudo make install
cd ..
git clone https://github.com/readyready15728/dot-vimrc
cd
ln -s ~/src/dot-vimrc/.vimrc
mkdir ~/.vim
cd ~/.vim
ln -s ~/src/dot-vimrc/vundle.vim
cd
git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
vim -c 'PluginInstall' -c 'qa'
cd ~/.vim/bundle/YouCompleteMe
sudo apt install cmake npm
python3 install.py --java-completer --ts-completer

sudo apt install trash-cli

sudo apt install ocaml opam
opam init
eval `opam config env`
opam install core base utop merlin

cat << 'EOF' >> ~/.ocamlinit
#use "topfind";;
#thread;;
#require "core";;
EOF
```
