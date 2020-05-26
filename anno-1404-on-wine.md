# Anno 1404 on Wine
## Getting what is widely considered to be the best Anno game running on Linux

For me, finding the file `Engine.ini` and adding the key
`<DirectXVersion>9</DirectXVersion>` as mentioned
[here](https://appdb.winehq.org/objectManager.php?sClass=application&iId=9887)
was necessary but not sufficient. The additional step of running Wine like
this achieved the desired outcome:

```bash
PROTON_NO_D3D11=1 wine start Launch\ Anno\ 1404.lnk &
```

(N.b.: this is the GOG version of the game. Execution needs to be done this
way every time or the `DirectXVersion` key will be overwritten with a default
value.)
