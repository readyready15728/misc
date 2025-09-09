# Ranger Notes

## No longer using Midnight Commander

* `ranger --copy-config=all` to start with. Your configuration files can then
be found `~/.config/ranger/`.
* In the renaming dialogue, type `<Tab>` in order to fill in the existing
filename so it can be altered more easily, if desired.
* `S` enters shell.
* I added the [ranger-archives](https://github.com/maximtrp/ranger-archives)
plugin.
* ranger can in fact preview images directly in kitty for example but has to
do so outside of tmux, with `$TERM` set to `xterm-kitty` (or perhaps something
else like this. It's a costly gimmick not to work under tmux.
* `default_linemode sizehumanreadablemtime` is what I want.
* Set `EDITOR` and `VISUAL` to `vim` for desired results when editing files
(which I should have done regardless).
* Search is case-insensitive but **only if** no uppercase letters have been
entered.
* Beware of pasting files with the same name elsewhere because the behavior
with `pp` is to just add the file with an underscore attached to the end.
