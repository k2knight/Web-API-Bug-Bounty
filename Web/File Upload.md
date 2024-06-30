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

---

## Bypass Techniques

- Change Content-Type in Repeater
- blacklist bypass by giving related file name extensions (php --> php3/phtml)
- Suffix bypass `.php* (* -> 2-7)`  `.ph*  (pht,phtm,phtml)` `.php.gif` `.jpg%00.php`
- Upload `.htaccess` --> `SetHandler application/x-httpd-php` and upload original file as any non existent file extension like `.ppp` with content type `application/octet-stream`
- Case of suffix. Change the suffix case (php --> pHp/phP)
- give a empty space ` ` at the end of the file extension only if the target server is windows. windows will omit automatically if any space is there at the end of the file
- append `.` at the end of the file extension.if the target server is windows. windows will omit automatically if any `.` is there at the end of the file.
- `abc.php::$DATA` in windows systems only. DATA is the fefault attribute for NTFS.
- append `. .`  for windows.
- 