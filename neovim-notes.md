# Neovim Notes
## Notes on Neovim, which I'm not sure I want to switch to yet

* Start here: https://lazyvim-ambitious-devs.phillips.codes/
* I needed `$TERM` set to `tmux-256color` for the `<Home>` and `<End>` keys to work.
* In the [LazyVim documentation for writing a colorscheme plugin](https://www.lazyvim.org/plugins/colorscheme), nothing is inherently required about the name `colorscheme.lua`. It could be any filename with the `.lua` extension.
* Refer to [LazyVim documentation on writing plugins](http://www.lazyvim.org/configuration/plugins) for how to make the [cyberdream.nvim](https://github.com/scottmckendry/cyberdream.nvim) colorscheme transparent in LazyVim. There is no need for any of the code that starts with `require("cyberdream").setup({`. Rather, the `opts` key is used with `transparent = true`.
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
* `S` for `Sync` in the `Lazy.nvim` plugin manager does install, clean and update in a single action.
* The LazyVim extras can be quite useful. Consider `editor.dial` which lets you increment and decrement strings like `December`, `2022/02/22`, `sixth`, and `Tuesday`.
* Use `:lua Snacks.dashboard()` to access the dashboard after starting Neovim.
* `gc` in normal mode (presumably also in Vim (actually, no, at least not by default)) toggles comments.
