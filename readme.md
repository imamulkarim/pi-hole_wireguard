## Pi-hole Configuration

### Install OpenSSH Client

- Go to Settings > Apps > Optional features.
- If "OpenSSH Client" is not listed under "Installed features," click "View features" or "Add an optional feature".
- In the search box, type "OpenSSH" and select the checkbox next to OpenSSH Client.
- Click "Next" and then "Install" to begin the installation. 

### Install OpenSSH Client

- Open Command Prompt or PowerShell.
- Type the command: ssh username@server_address (replace username with your remote username and server_address with the server's IP or hostname).
- If prompted, type yes to confirm the host key's fingerprint.
- Enter your password when prompted to log in.
- To connect to a specific port, use the -p flag: ssh username@server_address -p PortNumber

[Example](https://www.youtube.com/watch?v=d_3h5n9mPdI&t=11s)


### Install & Configure pi-hole 

    1. ssh admin@pihole
	2. enter pass - Asdf1234
	3  [Brose here to get pi hole cmd](https://docs.pi-hole.net/main/basic-install/)
	3. curl -sSL https://install.pi-hole.net | bash
	4. sudo pihole setpassword
	5. Pass - > A******4

### remember pi-hole mac and ip for future reference

- 2C:CF:67:D3:AA:46
- 192.168.1.237


[DNS Regex - youtube](https://www.youtube.com/watch?v=o-bxDuH_T6I)


- diproton-ads-[^\.]*\.hulu\.com\.akadns\.net
- ^ad([sxv]?[0-9]*|system)[_.-]([^.[:space:]]+\.){1,}|[_.-]ad([sxv]?[0-9]*|system)[_.-]
- ^(.+[_.-])?adse?rv(er?|ice)?s?[0-9]*[_.-]
- ^(.+[_.-])?telemetry[_.-]
- ^adim(age|g)s?[0-9]*[_.-]
- ^adtrack(er|ing)?[0-9]*[_.-]
- ^advert(s|is(ing|ements?))?[0-9]*[_.-]
- ^aff(iliat(es?|ion))?[_.-]
- ^analytics?[_.-]
- ^banners?[_.-]
- ^beacons?[0-9]*[_.-]
- ^count(ers?)?[0-9]*[_.-]
- ^mads\.
- ^pixels?[-.]
- ^stat(s|istics)?[0-9]*[_.-]
- ^https?://([A-Za-z0-9.-]*\.)?clicks\.beap\.bc\.yahoo\.com/
- ^https?://([A-Za-z0-9.-]*\.)?secure\.footprint\.net/
- ^https?://([A-Za-z0-9.-]*\.)?match\.com/
- ^https?://([A-Za-z0-9.-]*\.)?clicks\.beap\.bc\.yahoo(\.\w{2}\.\w{2}|\.\w{2,4})/
- ^https?://([A-Za-z0-9.-]*\.)?sitescout(\.\w{2}\.\w{2}|\.\w{2,4})/
- ^https?://([A-Za-z0-9.-]*\.)?appnexus(\.\w{2}\.\w{2}|\.\w{2,4})/
- ^https?://([A-Za-z0-9.-]*\.)?evidon(\.\w{2}\.\w{2}|\.\w{2,4})/
- ^https?://([A-Za-z0-9.-]*\.)?mediamath(\.\w{2}\.\w{2}|\.\w{2,4})/
- ^https?://([A-Za-z0-9.-]*\.)?scorecardresearch(\.\w{2}\.\w{2}|\.\w{2,4})/
- ^https?://([A-Za-z0-9.-]*\.)?doubleclick(\.\w{2}\.\w{2}|\.\w{2,4})/
- ^https?://([A-Za-z0-9.-]*\.)?flashtalking(\.\w{2}\.\w{2}|\.\w{2,4})/
- ^https?://([A-Za-z0-9.-]*\.)?turn(\.\w{2}\.\w{2}|\.\w{2,4})/
- ^https?://([A-Za-z0-9.-]*\.)?mathtag(\.\w{2}\.\w{2}|\.\w{2,4})/
- ^https?://([A-Za-z0-9.-]*\.)?googlesyndication(\.\w{2}\.\w{2}|\.\w{2,4})/
- ^https?://([A-Za-z0-9.-]*\.)?s\.yimg\.com/cv/ae/us/audience/
- ^https?://([A-Za-z0-9.-]*\.)?clicks\.beap/
- ^https?://([A-Za-z0-9.-]*\.)?.doubleclick(\.\w{2}\.\w{2}|\.\w{2,4})/
- ^https?://([A-Za-z0-9.-]*\.)?yieldmanager(\.\w{2}\.\w{2}|\.\w{2,4})/
- ^https?://([A-Za-z0-9.-]*\.)?w55c(\.\w{2}\.\w{2}|\.\w{2,4})/
- ^https?://([A-Za-z0-9.-]*\.)?adnxs(\.\w{2}\.\w{2}|\.\w{2,4})/
- ^https?://([A-Za-z0-9.-]*\.)?advertising\.com/
- ^https?://([A-Za-z0-9.-]*\.)?evidon\.com/
- ^https?://([A-Za-z0-9.-]*\.)?scorecardresearch\.com/
- ^https?://([A-Za-z0-9.-]*\.)?flashtalking\.com/
- ^https?://([A-Za-z0-9.-]*\.)?turn\.com/
- ^https?://([A-Za-z0-9.-]*\.)?mathtag\.com/
- ^https?://([A-Za-z0-9.-]*\.)?surveylink/
- ^https?://([A-Za-z0-9.-]*\.)?info\.yahoo\.com/
- ^https?://([A-Za-z0-9.-]*\.)?ads\.yahoo\.com/
- ^https?://([A-Za-z0-9.-]*\.)?global\.ard\.yahoo\.com/


### Some DNS List
-[gist.githubusercontent.com/anudeepND](https://gist.githubusercontent.com/anudeepND/adac7982307fec6ee23605e281a57f1a/raw/5b8582b906a9497624c3f3187a49ebc23a9cf2fb/Test.txt)
-[blocklistproject.github.io](https://blocklistproject.github.io/Lists/ads.txt)

-[Local Url - anudeepND](https://github.com/imamulkarim/pi-hole_wireguard/blob/main/pi-hole/anudeepND.txt)
-[Local Url - blocklistproject](https://github.com/imamulkarim/pi-hole_wireguard/blob/main/pi-hole/ads.txt)