Setup Steps (Pi Zero 2 W)
1. Keep Pi‑hole Running
- Pi‑hole already listens on port 53 (DNS).
- Leave it as your DNS resolver.
2. Install Squid + E2Guardian

sudo apt update
sudo apt install squid e2guardian

sudo nano /etc/squid/squid.conf

## Configure Squid - Edit /etc/squid/squid.conf.
- Enable transparent proxy mode and

1. Remove existing Squid
sudo systemctl stop squid
sudo apt purge squid squid-common squid-openssl -y
sudo rm -rf /etc/squid /var/lib/squid

2. Istall build dependencies
sudo apt update
sudo apt install build-essential libssl-dev pkg-config wget tar -y

3. Download Squid source
sudo wget https://github.com/squid-cache/squid/archive/refs/tags/SQUID_7_3.tar.gz
tar -xvzf SQUID_7_3.tar.gz
cd SQUID_7_3
cd src

sudo apt install autoconf automake libtool pkg-config -y
wget https://www.squid-cache.org/Versions/v7/squid-7.3.tar.xz
tar -xvJf squid-7.3.tar.xz
cd squid-7.3
./configure --with-openssl --enable-ssl-crtd --prefix=/usr --localstatedir=/var --sysconfdir=/etc/squid
make -j4
sudo make install


4. Configure with SSL bump support

./configure --with-openssl --enable-ssl-crtd --prefix=/usr --localstatedir=/var --sysconfdir=/etc/squid

5. Compile and install
make -j4
sudo make install

6. Create SSL database
sudo mkdir -p /var/lib/ssl_db
sudo /usr/libexec/security_file_certgen -c -s /var/lib/ssl_db -M 4MB
sudo chown -R proxy:proxy /var/lib/ssl_db

sudo mkdir -p /var/cache/squid/ssl_db
sudo /usr/libexec/security_file_certgen -c -s /var/cache/squid/ssl_db -M 4MB


7. Generate a CA certificate + key
sudo mkdir -p /etc/squid/ssl_cert
sudo openssl req -new -newkey rsa:2048 -days 3650 -nodes -x509 \
    -keyout /etc/squid/ssl_cert/myCA.pem \
    -out /etc/squid/ssl_cert/myCA.pem
sudo chown -R proxy:proxy /etc/squid/ssl_cert

8. Minimal working squid.conf
- Replace /etc/squid/squid.conf with
sudo nano /etc/squid/squid.conf

# Squid basic config with SSL bump
http_port 3128
http_port 3129 intercept
https_port 3130 intercept ssl-bump cert=/etc/squid/ssl_cert/myCA.pem key=/etc/squid/ssl_cert/myCA.pem

# SSL bump rules
acl step1 at_step SslBump1
ssl_bump peek step1
ssl_bump bump all

# Certificate generator
--cert_generate_program /usr/libexec/security_file_certgen -s /var/lib/ssl_db -M 4MB
--ssl_crtd_program /usr/libexec/security_file_certgen -s /var/lib/ssl_db -M 4MB

# Basic ACLs
acl localnet src 192.168.0.0/16
http_access allow localnet
http_access deny all

# Logging
access_log /var/log/squid/access.log
cache_log /var/log/squid/cache.log

9. Validate config
sudo squid -k parse

10. Start Squid
sudo /usr/sbin/squid  --start
sudo /usr/sbin/squid -k shutdown


# When Package installer used
sudo systemctl restart squid 
sudo systemctl status squid

10.1 alternate debug
sudo /usr/sbin/squid -N -d1


sudo apt install iptables

# Redirect HTTP
# Flush old rules
sudo iptables -F

- Replace wlan0 with your actual interface 
ip link show


sudo iptables -t nat -A PREROUTING -i wlan0 -p tcp --dport 80 -j REDIRECT --to-port 3129

# Redirect HTTPS
sudo iptables -t nat -A PREROUTING -i wlan0 -p tcp --dport 443 -j REDIRECT --to-port 3130


# Debuging
tail -f /var/log/squid/access.log
tail -f /var/log/squid/cache.log

## *********************************************************

## Configure E2Guardian with Squid as Upstream Proxy

# Edit E2Guardian Config

sudo nano /etc/e2guardian/e2guardian.conf

# E2Guardian listening port (clients connect here)
proxyport = 8080

# Upstream proxy (Squid)
proxyip = 127.0.0.1
proxyport = 3128

# Enable phrase and URL filtering
usephraselists = on
useurllists = on

sudo mkdir /etc/e2guardian/list/blacklists/

bannedurllist = '/etc/e2guardian/lists/blacklists/urls.txt'

sudo systemctl status e2guardian

# Debuging
tail -f /var/log/e2guardian/access.log