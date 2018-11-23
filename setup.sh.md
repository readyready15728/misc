# setup.sh
## Making a new installation comfy quickly

Self-explanatory. Got a new Pi? Just opened up a new cloud account? Here ya go:

```bash
#!/bin/sh

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
EOF

mkdir ~/src
cd ~/src
git clone https://github.com/vim/vim
cd vim
# Change this to suit taste, for example by enabling compilation of GVim
./configure --enable-python3interp=yes --enable-terminal --enable-multibyte
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
sudo apt install cmake
python3 install.py --js-completer --java-completer
```
