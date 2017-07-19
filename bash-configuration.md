The following will create an eternal history for bash as well as preserving
history from multiple terminal tabs and is drawn from the following Stack
Overflow questions:

[https://stackoverflow.com/questions/9457233/unlimited-bash-history]
[https://unix.stackexchange.com/questions/1288/preserve-bash-history-in-multiple-terminal-windows/]

```bash
export HISTFILESIZE=
export HISTSIZE=
export HISTTIMEFORMAT="[%F %T] "
export HISTFILE=~/.bash_eternal_history
PROMPT_COMMAND="history -a; history -c; history -r; $PROMPT_COMMAND"
```
