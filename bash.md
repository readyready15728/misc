# bash

* The following will create an eternal history for bash as well as preserving
history from multiple terminal tabs and is drawn from the following Stack
Overflow questions:

    * [https://stackoverflow.com/questions/9457233/unlimited-bash-history]
    * [https://unix.stackexchange.com/questions/1288/preserve-bash-history-in-multiple-terminal-windows/]

    ```bash
    export HISTFILESIZE=
    export HISTSIZE=
    export HISTTIMEFORMAT="[%F %T] "
    export HISTFILE=~/.bash_eternal_history
    PROMPT_COMMAND="history -a; history -c; history -r; $PROMPT_COMMAND"
    ```
* I have often found that when I searched backwards in history but hit the
wrong key (something I do frequently) I had to hold down the down arrow for a
long time to start over looking for that command again. I looked into this and
it's not actually not necessary. `M->` will take the user to the very end of
history without any tedium.
