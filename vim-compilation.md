# Vim Compilation
## Making the most of a great editor

Here is my "Cadillac" configuration of Vim:

```bash
./configure --enable-luainterp=yes --enable-perlinterp=yes --enable-python3interp=yes --enable-tclinterp=yes --enable-rubyinterp=yes --enable-terminal --enable-multibyte --enable-gui=gtk3
```

Maybe I'll actually even use the Tcl interface someday. Who knows?

(N.b. `--enable-pythoninterp=yes` and `--enable-python3interp=yes` should not
be used simultaneously as they will force dynamic loading of the first version
invoked and make `has('python')` and `has('python3')` both evaluate to zero.
