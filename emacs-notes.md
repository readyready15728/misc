# Emacs Notes

## **E**ight **M**egs **A**nd **C**onstantly **S**wapping

* `C-h t` opens the tutorial.
* `C-h r` opens the manual.
* Here's the [reference card](https://www.gnu.org/software/emacs/refcards/pdf/refcard.pdf).
* Here's the [wiki](https://www.emacswiki.org/emacs/SiteMap) and more specifically the [newbie page](https://www.emacswiki.org/emacs/EmacsNewbie).
* Other unofficial sources of documentation:
  * [Emacs Redux](https://emacsredux.com/)
  * [Emacs Rocks](https://emacsrocks.com/)
  * [Mastering Emacs](https://www.masteringemacs.org/)
  * [Pragmatic Emacs](https://pragmaticemacs.wordpress.com/) (inactive but presumably still useful)
  * [System Crafters](https://systemcrafters.net/)
* Running `./autogen.sh` is necessary after cloning the repository.
* `./configure` gives a comprehensive list of features enabled or not enabled
at the very end.
* There were a few things I had to install. Here is what I gave to `sudo apt install`:
  * `libacl1-dev`
  * `'libgccjit-*-dev'`
  * `libgnutls28-dev`
  * `libgpm-dev`
  * `libm17n-dev`
  * `libmagick++-dev` (not certain about this one because Emacs is written in C and Emacs Lisp, not C++)
  * `libmagickcore-dev`
  * `liboft-dev`
  * `libsystemd-dev`
  * `libtree-sitter-dev`
  * `mailutils`
* `libxft-dev` is not needed for anti-aliased text.
* `--with-xwidgets` (allows native widgets to be embedded in Emacs) appears broken for the time being.
* After installing dependencies I did `./configure --with-imagemagick --with-mailutils --with-tree-sitter`
* `C-x C-c` to `:wqa`.
* `C-g` to abort partially entered keystrokes or an entered command that is
taking too long.
* `C-l` cycles the display through three states: "centered on the current line",
"current line at the bottom", "current line at the top".
* `M-f` and `M-b` work just like in the shell.
* `C-a` and `C-e` are also the same.
* `M-a` and `M-e` move to the beginnings and ends of sentences, respectively.
* `M-<` and `M->` do `gg` and `G`, respectively.
* `C-u` to specify a numeric prefix argument.
* `C-x 2` does a horizontal split and `C-x 3` does a vertical split.
* `C-x 0` kills the current window.
* `C-x 1` kills all other windows.
* `C-x o` changes the current window.
* `M-d` works like in the shell.
* `C-x u` (and `C-/`) does undo.
* `C-k` works like in the shell.
* `M-k` kills to the end of the current sentence.
* `C-<SPC>` to set the mark then move the cursor where desired and then `C-w`
to kill the text between mark and cursor.
* `C-y` "yanks"" (basically "pastes") the last killed text.
* Several `C-k`s in a row count as one unified kill.
* `C-x C-f` opens ("finds") a file.
* `C-x C-s` does `:w` and `C-x s` does `:wa`.
* `C-x C-b` lists buffers.
* `C-x b` switches buffers.
* `C-z` minimizes graphical Emacs.
* `M-g g` does `goto-line`.
* Only one major mode can be active at a given time.
* Use `C-h m` to view the documentation on the current major mode.
* `C-x k` does `kill-buffer`.
* `C-x f` sets margin for `auto-fill-mode`.
* `C-s` and `C-r` do incremental search forwards and backwards, respectively.
* Case-insensitive search appears to be the default.
