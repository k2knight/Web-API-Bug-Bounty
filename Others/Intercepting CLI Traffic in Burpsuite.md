# Intercepting CLI Traffic in Burpsuite

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

Note: For some reasons proxychains is not working for all tools.
We need to use `http_proxy=localhost:8080 https_proxy=localhost:8080` before the command to intercept the traffic in burpsuite.

Alternative to this is to set the `http_proxy` for every **zshrc** shell. for that i adding these 2 line in `subl ~/.zshrc` --> `source ~/.zshrc`

```
alias setproxy='export http_proxy="http://localhost:8080" && export https_proxy="http://localhost:8080" && echo "Proxy set to Burpsuite"'
alias unsetproxy='unset http_proxy && unset https_proxy && echo "Proxy unset"'
```

From now use **setproxy** in the new shell when ever we wants to intercept the traffic from CLI tools.

To remove the proxy we can use **unsetproxy**.