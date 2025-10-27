# Neovim Notes

## Notes on Neovim

* Start here:
[https://lazyvim-ambitious-devs.phillips.codes/](https://lazyvim-ambitious-devs.phillips.codes/)
* I needed `$TERM` set to `tmux-256color` for the `<Home>` and `<End>` keys to
work.
* In the [LazyVim documentation for writing a colorscheme
plugin](https://www.lazyvim.org/plugins/colorscheme), nothing is inherently
required about the name `colorscheme.lua`. It could be any filename with the
`.lua` extension.
* Refer to [LazyVim documentation on writing
plugins](http://www.lazyvim.org/configuration/plugins) for how to make the
[cyberdream.nvim](https://github.com/scottmckendry/cyberdream.nvim)
colorscheme transparent in LazyVim. There is no need for any of the code that
starts with `require("cyberdream").setup({`. Rather, the `opts` key is used
with `transparent = true`.
* For altering the `whichwrap` option in `options.lua`, because it's a flag
list:

```lua
vim.opt.whichwrap:append({
  ["<"] = true,
  [">"] = true,
})
```

* Turning off `bufferline.nvim` in `config/plugins/disabled.lua`:

```lua
return {
  { "akinsho/bufferline.nvim", enabled = false },
}
```

* `S` for `Sync` in the `Lazy.nvim` plugin manager does install, clean and
update in a single action.
* The LazyVim extras can be quite useful. Consider `editor.dial` which lets
you increment and decrement strings like `December`, `2022/02/22`, `sixth`,
and `Tuesday`.
* Use `:lua Snacks.dashboard()` to access the dashboard after starting Neovim.
* `gc` in normal mode (presumably also in Vim (actually, no, at least not by
default)) toggles comments.
* Make more use of `I` and `A` and `C` and `D` in normal mode and mind the
difference between `^` and `0`.
* `<Ctrl>-o` does "go the place I jumped from". `<Ctrl>-i` does the opposite.
* `<Space><Space>` opens the "files in current project" picker.
* To open multiple files in the file picker, `<Tab>` the appropriate files
then hit `<Enter>`.
* "`<Space>ff` is the same as `<Space><Space>`. It opens 'Find Files (Root
Directory)' and is just another longer way to get there. I assume it exists in
both places so that users can choose to map some other action to to the
super-accessible `<Space><Space>` and still be able to access the picker
functionality through `<Space>ff`."
* "`<Space>fF`, where the second `F` is shifted, is slightly different; it is
mapped to an action called 'Find Files (cwd)'."
* "The snacks picker is inspired by the command line tool fzf which means
'fuzzy find'. This tool allows you to quickly access files and open
directories from your shell, and I highly recommend it.
* "Let's start by opening an explorer using the `<Space>e` keybinding, where
the mnemonic is '**e** for Explore'. If you pop up the Space mode menu, you’ll
see that, as with the picker, there are two ways to open the explorer:
`<Space>-e` for Explore Snacks (root directory) and `<Space>E` for Explore
Snacks (cwd).
* `?` opens the help for Explore Snacks.
* Use `<Backspace>` to go up one level in explorers.
* `(` and `)` move whole sentences.
* `[` and `]` invoke "Unimpaired Mode".
* "Instead of jumping out of square brackets as you might expect, the easy to
type `[[` and `]]` are reserved for a more common operation: jumping to other
references to the variable under the cursor (in the same file)."
* "The `[c`, `]c`, `[f`, `]f`, `[m`, and `]m` keybindings allow you to
navigate around a source code file by jumping to the previous or next
class/type definition, function definition, or method definition. The
usefulness of these features depends a bit on both the language you are using
and the way the Language Service for the language is configured, but it works
well in common languages."
* "Because I am so incredibly talented at introducing problems in my code, a
common navigation task I need to perform is 'jump to the next squiggly line'.
Collectively, these are referred to as **d**iagnostics, so the key
combinations are `[d` and `]d`. If you only want to focus on errors and ignore
hints and warnings, you can use `[e` and `]e`. Analogously, the `[w` and `]w`
keybindings navigate between only warnings."
* "`[h` and `]h` allow you to jump to the next git 'hunk'."
* If yanky.nvim is enabled from the extras menu, `<Space>p` opens the
clipboard history.
* "Another super useful keybinding is `[y`. If you invoke this command
immediately after a put operation, the text that was put will be replaced with
the text that was cut or copied prior to the most recent yank. And if you
press it again, it will go back one more step in history, up to 100 steps. So
if you aren't sure exactly which numbered register a delete operation is in,
or you want to access text that was yanked but is no longer in the `"0`
register, you can use `p[y[y[y` until you find the text you really wanted
to pasted. If you go too far, you can cycle forward with `]y`."
* "The `qQ` command to 'append to recording' operation is analogous to the
capitalized `A<command>` used to append to a register."
* "The `Q` command to play back a recording always plays back the most recently
recorded command, regardless of register. If you want to play back from a
different register, you would use the `@` command, followed by the name of the
register. So if you recorded using `qa`, you would play it back with `@a`. As a
shortcut, `@@` will always replay whichever register you most recently played
(which is different from `Q` which always plays back the most recent
recording)."
* `<Space><Comma>` is the author of the LazyVim book's preferred means of
interacting with buffers.
* `<Space>bD` does "close buffer and the window split it is in".
* `<Space>bo` does "close all buffers other than the active one".
* `<Esc>` appears to do `:nohlsearch`, at least with LazyVim.
* With autoformatting turned off, `gq` can be used to manually format code
according to a linter.
* `<Space>bD` (to close buffer) and `<Space>bD` to close buffer **and**
containing window.
* `<Ctrl>-w` and `<Space>w` both open the window menu.
* `<Space>ws` opens a horizontal split and `<Space>wv` opens a vertical split.
* In Neotree, `<Space>s` does a vertical split on the selected file and
`<Space>S` does a horizontal split.
* `<Space>qq` to save a session local to the current directory, `<Space>qs` to
restore the local session, and `<Space>qS` to look at any number of sessions
that have been made recently. Lastly, `<Space>qd` quits without disturbing the
existing session.
* `<Space>cm` opens the menu for mason.nvim.
* `<Space>cl` is a shortcut for `:LspInfo`, which displays information about
any language servers that are running and which buffers they are attached to.
* `:LspRestart` turns it off and on again.
* `:LazyHealth` and `:checkhealth` (to be used in that order) provide further
diagnostics.
* Use `<Space>cd` to expand on diagnostic text.
* Open the diagnostics/quick fix menu with `<Space>x`.
