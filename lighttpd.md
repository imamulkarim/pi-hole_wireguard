

## How to Configure Pi‑hole (lighttpd) with Your Squid Cert

sudo apt install lighttpd -y
sudo systemctl enable lighttpd
sudo systemctl start lighttpd
sudo systemctl status lighttpd

Verify Pi‑hole’s admin files
Check that the admin UI exists:
ls -lh /var/www/html/admin


4. Access the dashboard
- Default URL:
http://192.168.1.237/admin
- If you want HTTPS, configure lighttpd with your Squid certificate (as we discussed earlier). Otherwise, stick with HTTP.




sudo mkdir -p /etc/lighttpd/certs
sudo cp /etc/squid/ssl_cert/myCA.pem /etc/lighttpd/certs/pihole.pem


- Create or edit
sudo nano /etc/lighttpd/conf-enabled/10-ssl.conf
$SERVER["socket"] == ":443" {
    ssl.engine = "enable"
    ssl.pemfile = "/etc/lighttpd/certs/pihole.pem"
}

- Restart lighttpd:
sudo systemctl restart lighttpd
