Navigate to 
```
cd /etc/unbound/unbound.conf.d/
```
- make a copy of the already working config files.
```
sudo cp pi-hole.conf pi-hole.conf.back
```
- Edit the file for configuration
```
sudo nano pi-hole.conf
```
Add this code right at the end of the file `Ensure privacy of local IP Ranges:` block
```
#####################
# This section enables DoT (DNS over TLS)
#####################
#TLS cert bundle
    tls-cert-bundle: /etc/ssl/certs/ca-certificates.crt
#Connect to Cloudflare
    forward-zone:
    name: "."
    forward-tls-upstream: yes
    # Cloudflare DNS
    forward-addr: 2606:4700:4700::1111@853#cloudflare-dns.com
    forward-addr: 1.1.1.1@853#cloudflare-dns.com
    forward-addr: 2606:4700:4700::1001@853#cloudflare-dns.com
    forward-addr: 1.0.0.1@853#cloudflare-dns.com
```
![image](https://github.com/user-attachments/assets/b481499e-c7ed-4436-af49-fedcf5a6d14a) <br/>


- Restart the service:
```
sudo service unbound restart
```
