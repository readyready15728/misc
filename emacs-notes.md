# Emacs Notes

## **E**ight **M**egs **A**nd **C**onstantly **S**wapping

* `C-h t` opens the tutorial.
* `C-h r` opens the manual.
* Here's the [reference card](https://www.gnu.org/software/emacs/refcards/pdf/refcard.pdf).
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
* `libxft-dev` is not needed for anti-aliased text
* `--with-xwidgets` (allows native widgets to be embedded in Emacs) appears broken for the time being
* After installing dependencies I did `./configure --with-imagemagick --with-mailutils --with-tree-sitter`
