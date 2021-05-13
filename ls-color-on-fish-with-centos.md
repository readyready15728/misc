# ls Color on fish CentOS
## Grrr

I have no idea why it wasn't working. What helped was going into `$HOME/.config/fish/functions/ls.fish` and getting rid of this crap:

```fish
# Defined in /home/readyready15728/.config/fish/conf.d/config.fish @ line 5
function ls
 command ls ;
end
```

Then `ls --color` started working.
