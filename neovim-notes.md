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
* Make more use of `I` and `A` and `C` in normal mode and mind the difference
between `^` and `0`.
* `<Ctrl>-o` does "go the place I jumped from". `<Ctrl>-i` does the opposite.
* `<Space><Space>` opens the "files in current project" picker.
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
* "Let’s start by opening an explorer using the `<Space>-e` keybinding, where
the mnemonic is '**e** for Explore'. If you pop up the Space mode menu, you’ll see
that, as with the picker, there are two ways to open the explorer:
`<Space>-e` for Explore Snacks (root directory) and `<Space>-E` for Explore
Snacks (cwd).
* Use `<Backspace>` to go up one level in explorers.
* `(` and `)` move whole sentences.
* `[` and `]` invoke "Unimpaired Mode".
