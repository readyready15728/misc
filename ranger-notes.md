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
else like this). It's a costly gimmick not to work under tmux.
* `default_linemode sizehumanreadablemtime` is what I want.
* It's also possible to change the default view to orthodox instead of Miller
  panes with `set viewmode multipane`.
* The `--` for `xdg-open` that's in the default `rifle.conf` doesn't work and
to open `.epub` files properly with `xdg-open` I had to do
`xdg-mime default calibre-ebook-viewer.desktop application/epub+zip`.
* Handling `.pdf.xz` extensions was described in a [response to an issue from
me](https://github.com/ranger/ranger/issues/3190). Briefly, find the
"Archives" section in `rifle.conf` and make sure something like the following
comes first: `name pdf(\.xz)?$, has xreader, X, flag f = xreader -- "$@"`.
* Set `EDITOR` and `VISUAL` to `vim` for desired results when editing files
(which I should have done regardless).
* Search is case-insensitive but **only if** no uppercase letters have been
entered.
* Beware of pasting files with the same name elsewhere because the behavior
with `pp` is to just add the file with an underscore attached to the end.
