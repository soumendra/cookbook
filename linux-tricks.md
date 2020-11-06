# Linux Tricks

## Remap disfunctional keys in keyboard

1. Remap keys system-wide

https://askubuntu.com/questions/296155/how-can-i-remap-keyboard-keys

2. Remap keys in vscode

Vscode doesn't seem to respect OS bindings!

[Modify `settings.json` to include `"keyboard.dispatch": "keyCode"`!](https://github.com/microsoft/vscode/issues/23991)

## Split-download-combine a large file from a server

```text
from shutil import make_archive
make_archive("data", 'zip', "folder-to-be-zipped/")

!split --verbose -d -a 3 -b 95MB data.zip zip_large.

cat zip_large.??? > data.zip
```

