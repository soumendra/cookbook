## Split-download-combine a large file from a server

```text
from shutil import make_archive
make_archive("data", 'zip', "folder-to-be-zipped/")

!split --verbose -d -a 3 -b 95MB data.zip zip_large.

cat zip_large.??? > data.zip
```
