# Intercepting CLI Traffic in Burpsuite

```
subl ~/.zshrc
```

add these in the zshrc file

```
export http_proxy=localhost:8080
export https_proxy=localhost:8080
```

Installing Burp Certificate in kali as root (SYSTEM)

```
wget -O burpca.der http://localhost:8080/cert
openssl x509 -inform DER -in burpca.der -out burpca.crt
```

Now copy the burpca.crt to `/usr/local/share/ca-certificates/` 

```
sudo mv burpca.crt /usr/local/share/ca-certificates/burpca.crt
sudo update-ca-certificates
```

Certificate has been installed successful.

### How to access

By directly prepending the proxy
```
http_proxy=localhost:8080 https_proxy=localhost:8080 curl https://ifconfig.io
```

Using proxy chains

```
proxychains curl https://ifconfig.io
```

