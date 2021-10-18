# WifiRSAAuthenticationService

It is a web site for Wifi Authentication with RSA signature make by Debian 11. wifi hotspot is make by hostapt

## Demo

![image](https://user-images.githubusercontent.com/57281249/137624898-3a2d96b5-78d3-486d-a2ae-c88e2642bc50.png)

## Install

1. clone this repo and cd into WifiRSAAuthenticationService.

```bash
git clone https://github.com/Jimmy01240397/WifiRSAAuthenticationService
cd WifiRSAAuthenticationService
```

2. move wifilogn dir to /var/www .

```bash
mv wifilogin /var/www
```

3. make private and public key with openssl.

```bash
openssl genrsa -out client-private.key 2048
openssl rsa -in client-private.key -pubout -out client.pem
```

4. copy your public key to allowkey and send your private key to your mobile.

```bash
cp client.pem allowkey/
```

5. set up iptables rules according to the file "rules.v4" 

```bash
# or you can just 
iptables-restore rules.v4
# to set up the rules
```

6. **fix your work dir in wifiallowlist.sh and wifiallowremove.sh  (for me is /etc/WifiRSAAuthenticationService**
7. set up iptables log config **remember fix your work dir in config (for me is /etc/WifiRSAAuthenticationService** and restart rsyslog

```bash
mv iptableswlanlog.conf /etc/rsyslog.d/iptableswlanlog.conf
/etc/init.d/rsyslog restart
```

8. request your certificate from ca (or you can just use self signed certificate
9. put your server certificate and server private in dir name to server.crt and server.key

```bash
cp cert.crt server.crt
cp key.key server.key
```


10. move wifiallowweb.service to /lib/systemd/system/wifiallowweb.service **remember fix your work dir in wifiallowweb.service (for me is /etc/WifiRSAAuthenticationService**

```bash
mv wifiallowweb.service /lib/systemd/system/wifiallowweb.service
```

11. install python packet.

```bash
pip install Flask
pip install pycrypto
```

12. enable and start your server

```bash
systemctl enable wifiallowweb.service
systemctl start wifiallowweb.service

#when you have add public key in allowkey remember to restart the server
systemctl restart wifiallowweb.service
```
