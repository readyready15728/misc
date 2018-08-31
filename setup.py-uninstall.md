# Uninstall Packages Installed by `setup.py`
## Sometimes Stack Overflow is actually helpful

This is probably the best way to do it:

```bash
sudo python setup.py install --record files.txt
# inspect files.txt to make sure it looks ok. Then:
tr '\n' '\0' < files.txt | xargs -0 sudo rm -f --
```

(Stolen from Stack Overflow: https://stackoverflow.com/a/25209129/2663150)
