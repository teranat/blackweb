# [Blackweb](https://www.maravento.com/p/blackweb.html)

[![GPL v3+](https://img.shields.io/badge/License-GPL%20v3%2B-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)
[![last commit](https://img.shields.io/github/last-commit/maravento/blackweb)](https://github.com/maravento/blackweb/)
[![Twitter Follow](https://img.shields.io/twitter/follow/maraventostudio.svg?style=social)](https://twitter.com/maraventostudio)

**Blackweb** is a project that collects and unifies public blocklists of domains (porn, downloads, drugs, malware, spyware, trackers, bots, social networks, warez, weapons, etc.) to make them compatible with [Squid-Cache](http://www.squid-cache.org/)

**Blackweb** es un proyecto que recopila y unifica listas públicas de bloqueo de dominios (porno, descargas, drogas, malware, spyware, trackers, bots, redes sociales, warez, armas, etc.) para hacerlas compatibles con [Squid-Cache](http://www.squid-cache.org/)

## DATA SHEET

---

|ACL|Blocked Domains|File Size|
| :---: | :---: | :---: |
|blackweb.txt|5024038|128,9 MB|

## GIT CLONE

---

```bash
git clone --depth=1 https://github.com/maravento/blackweb.git
```

## HOW TO USE

---

**blackweb.txt** is already updated and optimized for [Squid-Cache](http://www.squid-cache.org/). Download it and unzip it in the path of your preference and activate [Squid-Cache RULE](https://github.com/maravento/blackweb#regla-squid-cache--squid-cache-rule) / **blackweb.txt** ya viene actualizada y optimizada para [Squid-Cache](http://www.squid-cache.org/). Descárguela y descomprimala en la ruta de su preferencia y active la [REGLA de Squid-Cache](https://github.com/maravento/blackweb#regla-squid-cache--squid-cache-rule)

### Download

```bash
wget -q -N https://raw.githubusercontent.com/maravento/blackweb/master/blackweb.tar.gz && cat blackweb.tar.gz* | tar xzf -
```

### Checksum

```bash
wget -q -N https://raw.githubusercontent.com/maravento/blackweb/master/checksum.md5
md5sum blackweb.txt | awk '{print $1}' && cat checksum.md5 | awk '{print $1}'
```

### [Squid-Cache](http://www.squid-cache.org/) Rule

---

Edit: / Edite:

```bash
/etc/squid/squid.conf
```

And add the following lines: / Y agregue las siguientes líneas:

```bash
# INSERT YOUR OWN RULE(S) HERE TO ALLOW ACCESS FROM YOUR CLIENTS
acl blackweb dstdomain "/path_to/blackweb.txt"
http_access deny blackweb
```

### [Squid-Cache](http://www.squid-cache.org/) Advanced Rules (recommended) / Reglas Avanzadas (recomendadas)

**Blackweb** contains millions of domains, therefore it is recommended: / **Blackweb** contiene millones de dominios, por tanto se recomienda:

- Use `allowdomains.txt` to exclude domains (e.g.: accounts.youtube.com [since Feb 2014, Google uses the subdomain accounts.youtube.com to authenticate its services](http://wiki.squid-cache.org/ConfigExamples/Streams/YouTube)) or false positives / Usar `allowdomains.txt` para excluir dominios (ejemplo: accounts.youtube.com [desde Feb 2014, Google utiliza el subdominio accounts.youtube.com para autenticar sus servicios](http://wiki.squid-cache.org/ConfigExamples/Streams/YouTube)) o falsos positivos

```bash
acl allowdomains dstdomain "/path_to/allowdomains.txt"
http_access allow allowdomains
```

- Use `blockdomains.txt` to add domains not included in `blackweb.txt` (e.g.: .youtube.com .googlevideo.com, .ytimg.com, etc) / Usar `blockdomains.txt` para agregar dominios no incluidos en `blackweb.txt` (ejemplo: .youtube.com .googlevideo.com, .ytimg.com, etc.)

```bash
acl blockdomains dstdomain "/path_to/blockdomains.txt"
http_access deny blockdomains
```

- Use `blocktlds.txt` to block Top Level Domains (TLDs) and country code (ccTLDs) / Use `blocktlds.txt` para bloquear Top Level Domains (TLD) y country code (ccTLD)

```bash
acl blocktlds dstdomain "/path_to/blocktlds.txt"
http_access deny blocktlds
```

URLs requests:

```bash
https://www.bardomain.xxx
https://subdomain.bardomain.xxx
https://www.bardomain.ru
https://www.bardomain.adult
https://www.foodomain.com
https://www.foodomain.porn
```

Squid Block:

```bash
.adult
.porn
.foodomain.com
.ru
.xxx
```

#### Advanced Rules Summary

```bash
# INSERT YOUR OWN RULE(S) HERE TO ALLOW ACCESS FROM YOUR CLIENTS
# Allow Domains
acl allowdomains dstdomain "/path_to/allowdomains.txt"
http_access allow allowdomains
# Block Domains
acl blockdomains dstdomain "/path_to/blockdomains.txt"
http_access deny blockdomains
# Block TLD/ccTLD
acl blocktlds dstdomain "/path_to/blocktlds.txt"
http_access deny blocktlds
# Blackweb
acl blackweb dstdomain "/path_to/blackweb.txt"
http_access deny blackweb
```

## IMPORTANT

**Blackweb** is designed exclusively for [Squid-Cache](http://www.squid-cache.org/) and due to the large number of blocked domains it is not recommended to use it in other environments ([DNSMasq](https://en.wikipedia.org/wiki/Dnsmasq), [Pi-Hole](https://pi-hole.net/), [Hosts File](https://en.wikipedia.org/wiki/Hosts_(file)), etc.), as it could slow it down or block it. **Use it at your own risk** / Blackweb está diseñado exclusivamente para [Squid-Cache](http://www.squid-cache.org/) y debido a la gran cantidad de dominios bloqueados no se recomienda usarlo en otros entornos ([DNSMasq](https://es.wikipedia.org/wiki/Dnsmasq), [Pi-Hole](https://pi-hole.net/), [Hosts File](https://es.wikipedia.org/wiki/Archivo_hosts), etc.), ya que podría ralentizarlo o bloquearlo. **Úselo bajo su propio riesgo**

For more information check [Issue 10](https://github.com/maravento/blackweb/issues/10#issuecomment-650834301)

## UPDATE

---

### ⚠️ WARNING: BEFORE YOU CONTINUE

This section is only to explain how update and optimization process works. It is not necessary for user to run it. This process can take time and consume a lot of hardware and bandwidth resources, therefore it is recommended to use test equipment / Esta sección es únicamente para explicar cómo funciona el proceso de actualización y optimización. No es necesario que el usuario la ejecute. Este proceso puede tardar y consumir muchos recursos de hardware y ancho de banda, por tanto se recomienda usar equipos de pruebas

#### Blackweb Update

>The update process of `blackweb.txt` consists of several steps and is executed in sequence by the script `bwupdate.sh` / El proceso de actualización de `blackweb.txt` consta de varios pasos y es ejecutado en secuencia por el script `bwupdate.sh`

```bash
wget -q -N https://raw.githubusercontent.com/maravento/blackweb/master/bwupdate/bwupdate.sh && chmod +x bwupdate.sh && ./bwupdate.sh
```

#### Dependencies

```bash
pkgs='wget git subversion curl libnotify-bin idn2 perl tar rar unrar unzip zip python-is-python2 squid'
if ! dpkg -s $pkgs >/dev/null 2>&1; then
  apt-get install $pkgs
fi
```

#### Bandwidth Check (optional)

>To guarantee update execution, before starting, script check bandwidth (with [Speedtest](https://raw.githubusercontent.com/sivel/speedtest-cli/master/speedtest.py)). If it is > 1 Mbit/s, update continues; else, it shows warning messages and it is recommended to interrupt update / Para garantizar la ejecución de la actualización, antes de comenzar, el script verifica el acho de banda (con [Speedtest](https://raw.githubusercontent.com/sivel/speedtest-cli/master/speedtest.py)). Si es > 1 Mbit/s, la actualización continúa; de lo contrario, muestra mensajes de advertencia y se recomienda interrumpir la actualización

#### Capture Public Blocklists

>Capture domains from downloaded public blocklists (see [SOURCES](https://github.com/maravento/blackweb#fuentes--sources)) and unifies them in a single file / Captura los dominios de las listas de bloqueo públicas descargadas (ver [FUENTES](https://github.com/maravento/blackweb#fuentes--sources)) y las unifica en un solo archivo

#### Domain Debugging

>Remove overlapping domains (`'.sub.example.com' is a subdomain of '.example.com'`), does homologation to Squid-Cache format and excludes false positives (google, hotmail, yahoo, etc.) with a allowlist (`allowurls.txt`) / Elimina dominios superpuestos (`'.sub.example.com' es un dominio de '.example.com'`), hace la homologación al formato de Squid-Cache y excluye falsos positivos (google, hotmail, yahoo, etc.) con una lista de permitidos (`allowurls.txt`)

```bash
com
.com
.domain.com
domain.com
0.0.0.0 domain.com
127.0.0.1 domain.com
::1 domain.com
domain.com.co
foo.bar.subdomain.domain.com
.subdomain.domain.com.co
www.domain.com
www.foo.bar.subdomain.domain.com
domain.co.uk
xxx.foo.bar.subdomain.domain.co.uk
```

outfile:

```bash
.domain.com
.domain.com.co
.domain.co.uk
```

#### TLD Validation

>Remove domains with invalid TLDs (with a list of Public and Private Suffix TLDs: ccTLD, ccSLD, sTLD, uTLD, gSLD, gTLD, eTLD, etc., up to 4th level 4LDs) / Elimina dominios con TLD inválidos (con una lista de TLDs Public and Private Suffix: ccTLD, ccSLD, sTLD, uTLD, gSLD, gTLD, eTLD, etc., hasta 4to nivel 4LDs)

```bash
.domain.exe
.domain.com
```

outfile:

```bash
.domain.com
```

#### Debugging Punycode-IDN

>Remove hostnames larger than 63 characters ([RFC 1035](https://www.ietf.org/rfc/rfc1035.txt)) and other characters inadmissible by [IDN](http://www.gnu.org/s/libidn/manual/html_node/Invoking-idn.html) and convert domains with international characters (not ASCII) and used for [homologous attacks](https://es.qwerty.wiki/wiki/IDN_homograph_attack) to [Punycode/IDNA](https://www.charset.org/punycode) format / Elimina hostnames mayores a 63 caracteres ([RFC 1035](https://www.ietf.org/rfc/rfc1035.txt)) y otros caracteres inadmisibles por [IDN](http://www.gnu.org/s/libidn/manual/html_node/Invoking-idn.html) y convierte dominios con caracteres internacionales (no ASCII) y usados para [ataques homográficos](https://es.qwerty.wiki/wiki/IDN_homograph_attack) al formato [Punycode/IDNA](https://www.charset.org/punycode)

```bash
.президент.рф
.mañana.com
.bücher.com
.café.fr
.köln-düsseldorfer-rhein-main.de
.mūsųlaikas.lt
.sendesık.com
```

outfile:

```bash
.xn--d1abbgf6aiiy.xn--p1ai
.xn--maana-pta.com
.xn--bcher-kva.com
.xn--caf-dma.fr
.xn--kln-dsseldorfer-rhein-main-cvc6o.de
.xn--mslaikas-qzb5f.lt
.xn--sendesk-wfb.com
```

#### DNS Loockup

>Most of the [SOURCES](https://github.com/maravento/blackweb#fuentes--sources) contain millions of invalid and nonexistent domains (see [internet live stats](https://www.internetlivestats.com/total-number-of-websites/)). Then, a triple check of each domain is done (in 3 steps) via DNS and invalid and nonexistent are excluded from Blackweb. This process may take. By default it processes domains in parallel ≈ 6k to 12k x min, depending on the hardware and bandwidth / La mayoría de las [FUENTES](https://github.com/maravento/blackweb#fuentes--sources) contienen millones de dominios inválidos e inexistentes (vea [internet live stats](https://www.internetlivestats.com/total-number-of-websites/)). Entonces se hace una verificación triple de cada dominio (en 3 pasos) vía DNS y los inválidos e inexistentes se excluyen de Blackweb. Este proceso puede tardar. Por defecto procesa en paralelo dominios ≈ 6k a 12k x min, en dependencia del hardware y ancho de banda

```bash
HIT google.com
FAULT testfaultdomain.com
```

#### Run Squid-Cache with Blackweb

>Run Squid-Cache with Blackweb and any error sends it to `SquidError.txt` on your desktop / Corre Squid-Cache con Blackweb y cualquier error lo envía a `SquidError.txt` en su escritorio

#### Check execution (/var/log/syslog):

```bash
Blackweb: Done 06/05/2019 15:47:14
```

#### Important about Blackweb Update

- The default path of **blackweb** is `/etc/acl`. You can change it for your preference / El path por default de **blackweb** es `/etc/acl`. Puede cambiarlo por el de su preferencia
- `bwupdate.sh` includes lists of domains related to remote support (Teamviewer, Anydesk, logmein, etc). They are commented by default (unless their domains are in the [SOURCES](https://github.com/maravento/blackweb#fuentes--sources)). To block or exclude them you must activate the corresponding line in the script (# JOIN LIST), although is not recommended to avoid conflicts or false positives / `bwupdate.sh` incluye listas de dominios relacionados con soporte remoto (Teamviewer, Anydesk, logmein, etc). Están comentadas por defecto (excepto que sus dominios estén en las [FUENTES](https://github.com/maravento/blackweb#fuentes--sources)). Para bloquearlas o excluirlas debe activar la línea correspondiente en el script (# JOIN LIST), aunque no se recomienda para evitar conflictos o falsos positivos
- If you need to interrupt the execution of `bwupdate.sh` (ctrl + c) and it stopped at the **DNS Loockup** part (3 verification steps), it will restart at that point. If you stop it earlier, you will have to start from the beginning or modify the script manually so that it starts from the desired point / Si necesita interrumpir la ejecución de `bwupdate.sh` (ctrl + c) y se detuvo en la parte de **DNS Loockup** (3 pasos de verificación), reiniciará en ese punto. Si lo detiene antes deberá comenzar desde el principio o modificar el script manualmente para que inicie desde el punto deseado.
- During the execution of `bipupdate.sh` it will request privileges when needed / Durante la ejecución de `bipupdate.sh` solicitará privilegios cuando los necesite

## SOURCES

---

### BLOCKLISTS

#### Active

- [ABPindo indonesianadblockrules](https://raw.githubusercontent.com/ABPindo/indonesianadblockrules/master/subscriptions/abpindo.txt)
- [Adaway](https://adaway.org/hosts.txt)
- [Adblock Warning Removal List](https://easylist-downloads.adblockplus.org/antiadblockfilters.txt)
- [adblock-leadgenerator-list](https://github.com/Rpsl/adblock-leadgenerator-list)
- [Anti-WebMiner](https://raw.githubusercontent.com/greatis/Anti-WebMiner/master/blacklist.txt)
- [anudeepND Blocklist](https://github.com/anudeepND/blacklist) (included: [coinminer](https://raw.githubusercontent.com/anudeepND/blacklist/master/CoinMiner.txt), [adservers](https://raw.githubusercontent.com/anudeepND/blacklist/master/adservers.txt))
- [BBcan177 lists](https://github.com/BBcan177/) (included: [spammers](https://github.com/BBcan177/referrer-spam-blacklist), [minerchk hostlist](https://github.com/BBcan177/minerchk), [MS-2](https://gist.github.com/BBcan177/4a8bf37c131be4803cb2))
- [betterwebleon dga-feed](https://raw.githubusercontent.com/betterwebleon/slovenian-list/master/filters.txt)
- [bigdargon](https://raw.githubusercontent.com/bigdargon/hostsVN/master/hosts)
- [BlackJack8 iOSAdblockList](https://github.com/BlackJack8/iOSAdblockList) (included: [iOSAdblockList](https://raw.githubusercontent.com/BlackJack8/iOSAdblockList/master/Hosts.txt) and [webannoyances](https://github.com/BlackJack8/webannoyances/raw/master/ultralist.txt)
- [chadmayfield](https://github.com/chadmayfield) (included: [porn_all](https://raw.githubusercontent.com/chadmayfield/my-pihole-blocklists/master/lists/pi_blocklist_porn_all.list), [porn top](https://raw.githubusercontent.com/chadmayfield/pihole-blocklists/master/lists/pi_blocklist_porn_top1m.list))
- [Cibercrime-Tracker](http://cybercrime-tracker.net/all.php)
- [cobaltdisco Google-Chinese-Results-Blocklist](https://raw.githubusercontent.com/cobaltdisco/Google-Chinese-Results-Blocklist/master/GHHbD_perma_ban_list.txt)
- [crazy-max WindowsSpyBlocker](https://raw.githubusercontent.com/crazy-max/WindowsSpyBlocker/master/data/hosts/spy.txt)
- [DandelionSprout adfilt](https://raw.githubusercontent.com/DandelionSprout/adfilt/master/Alternate%20versions%20Anti-Malware%20List/AntiMalwareHosts.txt)
- [Dawsey21 List](https://github.com/Dawsey21/Lists)
- [Disconnect.me](https://disconnect.me/) (included: [simple_ad](https://s3.amazonaws.com/lists.disconnect.me/simple_ad.txt), [simple_malvertising](https://s3.amazonaws.com/lists.disconnect.me/simple_malvertising.txt), [simple_tracking](https://s3.amazonaws.com/lists.disconnect.me/simple_tracking.txt))
- [EasyList Bulgarian](http://stanev.org/abp/adblock_bg.txt)
- [EasyList Chinese CJX's Annoyance List](https://raw.githubusercontent.com/cjx82630/cjxlist/master/cjx-annoyance.txt)
- [EasyList Chinese](https://easylist-downloads.adblockplus.org/easylistchina.txt)
- [Easylist Czech/Slovak](https://raw.githubusercontent.com/tomasko126/easylistczechandslovak/master/filters.txt)
- [EasyList Hebrew](https://raw.githubusercontent.com/easylist/EasyListHebrew/master/EasyListHebrew.txt)
- [EasyList Icelandic](https://adblock.gardar.net/is.abp.txt)
- [EasyList Indonesian](https://raw.githubusercontent.com/heradhis/indonesianadblockrules/master/subscriptions/abpindo.txt)
- [EasyList Romanian](https://www.zoso.ro/pages/rolist.txt)
- [EasyList Russian](https://easylist-downloads.adblockplus.org/advblock.txt)
- [ethanr dns](https://bitbucket.org/ethanr/dns-blacklists/raw/8575c9f96e5b4a1308f2f12394abd86d0927a4a0/bad_lists/Mandiant_APT1_Report_Appendix_D.txt)
- [FadeMind Risk](https://raw.githubusercontent.com/FadeMind/hosts.extras/master/add.Risk/hosts)
- [FadeMind Spam](https://raw.githubusercontent.com/FadeMind/hosts.extras/master/add.Spam/hosts)
- [fanboy-adblock](https://github.com/ryanbr/fanboy-adblock)
- [firebog.net](firebog.net) (included: [AdguardDNS](https://v.firebog.net/hosts/AdguardDNS.txt), [Admiral](https://v.firebog.net/hosts/Admiral.txt), [BillStearns](https://v.firebog.net/hosts/BillStearns.txt), [Easylist](https://v.firebog.net/hosts/Easylist.txt), [Easyprivacy](https://v.firebog.net/hosts/Easyprivacy.txt), [Kowabit](https://v.firebog.net/hosts/Kowabit.txt), [Prigent-Ads](https://v.firebog.net/hosts/Prigent-Ads.txt), [Prigent-Malware](https://v.firebog.net/hosts/Prigent-Malware.txt), [Prigent-Phishing](https://v.firebog.net/hosts/Prigent-Phishing.txt), [Prigent-Crypto](https://v.firebog.net/hosts/Prigent-Crypto.txt), [Shalla-mal](https://v.firebog.net/hosts/Shalla-mal.txt), [WaLLy3K](https://v.firebog.net/hosts/static/w3kbl.txt))
- [frogeye](https://hostfiles.frogeye.fr/firstparty-trackers-hosts.txt)
- [gfmaster adblock-korea](https://raw.githubusercontent.com/gfmaster/adblock-korea-contrib/master/filter.txt)
- [Halt-and-Block-Mining](https://raw.githubusercontent.com/ruvelro/Halt-and-Block-Mining/master/HBmining.bat)
- [hBlock](https://hblock.molinero.dev/hosts_domains.txt)
- [hexxium](https://hexxiumcreations.github.io/threat-list/hexxiumthreatlist.txt)
- [hostsfile.mine.nu](https://hostsfile.mine.nu/hosts0.txt)
- [iploggerfilter](https://github.com/piperun/iploggerfilter)
- [Jawz101 Potencial Trackers](https://raw.githubusercontent.com/jawz101/potentialTrackers/master/potentialTrackers.csv)
- [Joelotz URL](https://raw.githubusercontent.com/joelotz/URL_Blacklist/master/blacklist.csv)
- [Joewein](http://www.joewein.de/sw/bl-text.htm)
- [KADhosts](https://raw.githubusercontent.com/azet12/KADhosts/master/KADhosts.txt)
- [malc0de](http://malc0de.com/bl/)
- [malspam emotet list](https://github.com/MBThreatIntel/malspam)
- [Malwaredomainlist Hosts](http://www.malwaredomainlist.com/hostslist/hosts.txt)
- [Matomo-org](https://github.com/matomo-org/referrer-spam-blacklist/blob/master/spammers.txt)
- [mitchellkrogza](https://github.com/mitchellkrogza) (included: [Badd-Boyz-Hosts](https://raw.githubusercontent.com/mitchellkrogza/Badd-Boyz-Hosts/master/domains), [Hacked Malware Web Sites](https://raw.githubusercontent.com/mitchellkrogza/The-Big-List-of-Hacked-Malware-Web-Sites/master/.dev-tools/_strip_domains/domains.txt), [Nginx Ultimate Bad Bot Blocker](https://raw.githubusercontent.com/mitchellkrogza/nginx-ultimate-bad-bot-blocker/master/_generator_lists/bad-referrers.list), [The Big List of Hacked Malware Web Sites](https://github.com/mitchellkrogza/The-Big-List-of-Hacked-Malware-Web-Sites/blob/master/hacked-domains.list), [Ultimate Hosts Blacklist](https://github.com/Ultimate-Hosts-Blacklist/Ultimate.Hosts.Blacklist/tree/master/hosts))
- [NanoFilters](https://github.com/NanoAdblocker/NanoFilters)
- [Netlab360 DGA Domains](https://data.netlab.360.com/feeds/dga/dga.txt)
- [NoCoin adblock list](https://github.com/hoshsadiq/adblock-nocoin-list)
- [nothingblock](https://github.com/dorxmi/nothingblock)
- [Oleksiig](https://raw.githubusercontent.com/oleksiig/Squid-BlackList/master/denied_ext.conf)
- [openphish](https://openphish.com/feed.txt)
- [OSINT.digitalside.it](https://osint.digitalside.it/Threat-Intel/lists/latestdomains.txt)
- [Perflyst](https://github.com/Perflyst) (included: [android-tracking](https://raw.githubusercontent.com/Perflyst/PiHoleBlocklist/master/android-tracking.txt), [SmartTV](https://raw.githubusercontent.com/Perflyst/PiHoleBlocklist/master/SmartTV.txt))
- [Peter Lowe’s Ad and tracking server list](http://pgl.yoyo.org/adservers/serverlist.php?hostformat=nohtml)
- [phishing.army](https://phishing.army/download/phishing_army_blocklist_extended.txt)
- [Prebake - Filter Obtrusive Cookie Notices](https://raw.githubusercontent.com/liamja/Prebake/master/obtrusive.txt)
- [Public-Intelligence-Feeds - dom-bl](https://github.com/CriticalPathSecurity/Public-Intelligence-Feeds/)
- [Quedlin](https://github.com/quedlin/blacklist/blob/master/domains)
- [quidsup](https://gitlab.com/quidsup) (included: [notrack-blocklists](https://gitlab.com/quidsup/notrack-blocklists/raw/master/notrack-blocklist.txt), [notrack-malware](https://gitlab.com/quidsup/notrack-blocklists/raw/master/notrack-malware.txt))
- [Ransomware Database](https://docs.google.com/spreadsheets/u/1/d/1TWS238xacAto-fLKh1n5uTsdijWdCEsGIM0Y0Hvmc5g/pubhtml#)
- [reddestdream](https://reddestdream.github.io/Projects/MinimalHosts/etc/MinimalHostsBlocker/minimalhosts)
- [securemecca.net and hostsfile.org](https://hostsfile.org/Downloads/hosts.txt)
- [Someonewhocares](http://someonewhocares.org/hosts/hosts)
- [StevenBlack](https://github.com/StevenBlack) (included: [add.2o7Net](https://raw.githubusercontent.com/StevenBlack/hosts/master/data/add.2o7Net/hosts), [add.Risk](https://raw.githubusercontent.com/StevenBlack/hosts/master/data/add.Risk/hosts), [fakenews-gambling-porn-social](https://raw.githubusercontent.com/StevenBlack/hosts/master/alternates/fakenews-gambling-porn-social/hosts), [hosts](https://raw.githubusercontent.com/StevenBlack/hosts/master/hosts), [spam](https://raw.githubusercontent.com/StevenBlack/hosts/master/data/add.Spam/hosts), [uncheckyAds](https://raw.githubusercontent.com/StevenBlack/hosts/master/data/UncheckyAds/hosts))
- [Stopforumspam Toxic Domains](https://www.stopforumspam.com/downloads/toxic_domains_whole.txt)
- [Taz SpamDomains](http://www.taz.net.au/Mail/SpamDomains)
- [txthinking](https://raw.githubusercontent.com/txthinking/blackwhite/master/black.list)
- [Université Toulouse 1 Capitole - Blacklists UT1](https://dsi.ut-capitole.fr/blacklists/index_en.php)
- [URLhaus Malicious URL Blocklist](https://gitlab.com/curben/urlhaus-filter/raw/master/urlhaus-filter.txt)
- [vokins yhosts](https://raw.githubusercontent.com/vokins/yhosts/master/hosts)
- [Web Annoyances Ultralist](https://github.com/yourduskquibbles/webannoyances)
- [Winhelp2002](http://winhelp2002.mvps.org/hosts.txt)
- [YousList](https://raw.githubusercontent.com/yous/YousList/master/youslist.txt)
- [zerodot1 CoinBlockerLists](https://gitlab.com/ZeroDot1/CoinBlockerLists) (included: [Host](https://zerodot1.gitlab.io/CoinBlockerLists/hosts), [host_browser](https://zerodot1.gitlab.io/CoinBlockerLists/hosts_browser), [host_optional](https://zerodot1.gitlab.io/CoinBlockerLists/hosts_optional), [list](https://zerodot1.gitlab.io/CoinBlockerLists/list.txt), [list_browser](https://zerodot1.gitlab.io/CoinBlockerLists/list_browser.txt), [list_browser_UBO](https://zerodot1.gitlab.io/CoinBlockerLists/list_browser_UBO.txt))

#### Inactive, Discontinued or Private

*Recovered by [Wayback Machine](https://archive.org/web/), debugged and added to `oldurls.txt`*

- [280blocker](https://280blocker.net/files/280blocker_domain.txt)
- [adblockplus malwaredomains_full](https://easylist-downloads.adblockplus.org/malwaredomains_full.txt)
- [BambenekConsulting](http://osint.bambenekconsulting.com/feeds/dga-feed.txt)
- [Carl Spam](http://www.carl.net/spam/access.txt)
- [cedia.org.ec](https://mirror.cedia.org.ec) (included: [domains](https://mirror.cedia.org.ec/malwaredomains/domains.txt), [immortal_domains](https://mirror.cedia.org.ec/malwaredomains/immortal_domains.txt))
- [CHEF-KOCH BarbBlock-filter-list](https://github.com/CHEF-KOCH/BarbBlock-filter-list)
- [dshield.org](http://www.dshield.org) (included: [Low](http://www.dshield.org/feeds/suspiciousdomains_Low.txt), [Medium](https://www.dshield.org/feeds/suspiciousdomains_Medium.txt), [High](https://www.dshield.org/feeds/suspiciousdomains_High.txt))
- [Easylist Latvian](https://notabug.org/latvian-list/adblock-latvian/raw/master/lists/latvian-list.txt)
- [firebog.net](firebog.net) (included: [Airelle-hrsk](https://v.firebog.net/hosts/Airelle-hrsk.txt), [Airelle-trc](https://v.firebog.net/hosts/Airelle-trc.txt))
- [hosts-file.net](https://hosts-file.net) (included: [ad_servers](https://hosts-file.net/ad_servers.txt), [emd](https://hosts-file.net/emd.txt), [grm](https://hosts-file.net/grm.txt), [hosts](http://hosts-file.net/download/hosts.txt), [psh](https://hosts-file.net/psh.txt))
- [Malware Domains](http://mirror1.malwaredomains.com/files/justdomains)
- [margevicius easylistlithuania](http://margevicius.lt/easylistlithuania.txt)
- [MESD](http://squidguard.mesd.k12.or.us/blacklists.tgz)
- [Neohost](https://hosts.nfz.moe/full/hosts)
- [Passwall SpamAssassin](http://www.passwall.com/blacklist.txt)
- [Ransomware Abuse (Ransomware Tracker has been discontinued on Dec 8th, 2019)](https://ransomwaretracker.abuse.ch/blocklist/) (included: [CryptoWall](https://ransomwaretracker.abuse.ch/downloads/CW_C2_DOMBL.txt), [Locky](https://ransomwaretracker.abuse.ch/downloads/LY_C2_DOMBL.txt), [Domain Blocklist](https://ransomwaretracker.abuse.ch/downloads/RW_DOMBL.txt), [Ransomware Abuse](https://ransomwaretracker.abuse.ch/downloads/RW_URLBL.txt) ,[URL Blocklist ](https://ransomwaretracker.abuse.ch/downloads/TC_C2_DOMBL.txt),[TorrentLocker](https://ransomwaretracker.abuse.ch/downloads/TL_C2_DOMBL.txt))
- [Shallalist.de](http://www.shallalist.de/Downloads/shallalist.tar.gz)
- [squidblacklist.org](https://www.squidblacklist.org/) (included: [dg-ads](https://www.squidblacklist.org/downloads/dg-ads.acl), [dg-malicious.acl](https://www.squidblacklist.org/downloads/dg-malicious.acl))
- [tankmohit UnifiedHosts](https://raw.githubusercontent.com/tankmohit/UnifiedHosts/master/hosts.all)
- [UrlBlacklist](https://web.archive.org/web/*/http://urlblacklist.com)
- [Zeustracker](https://zeustracker.abuse.ch/blocklist.php?download=squiddomain)

### ALLOWLISTS (URL/TLD)

#### Active

- [iana](https://data.iana.org/TLD/tlds-alpha-by-domain.txt)
- [ipv6-hosts](https://raw.githubusercontent.com/lennylxx/ipv6-hosts/master/hosts) (Partial)
- [publicsuffix](https://raw.githubusercontent.com/publicsuffix/list/master/public_suffix_list.dat)
- [University Domains and Names Data List](https://raw.githubusercontent.com/Hipo/university-domains-list/master/world_universities_and_domains.json)
- [whoisxmlapi](https://www.whoisxmlapi.com/support/supported_gtlds.php)

#### Inactive, Discontinued or Private

*Recovered by [Wayback Machine](https://archive.org/web/), debugged and added to `allowurls.txt`*

- [O365IPAddresses](https://support.content.office.net/en-us/static/O365IPAddresses.xml) ([No longer support](ocs.microsoft.com/es-es/office365/enterprise/urls-and-ip-address-ranges?redirectSourcePath=%252fen-us%252farticle%252fOffice-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2))

### Debug

- [Allow URLs](https://github.com/maravento/blackweb/tree/master/bwupdate/lst)
- [Block URLs](https://github.com/maravento/blackweb/tree/master/bwupdate/lst)
- [Block TLDs](https://github.com/maravento/blackweb/tree/master/bwupdate/lst)
- [Invalid TLDs](https://github.com/maravento/blackweb/tree/master/bwupdate/lst)
- [Old URls](https://github.com/maravento/blackweb/tree/master/bwupdate/lst)
- [Remote](https://github.com/maravento/blackweb/tree/master/bwupdate/lst)

### Worktools

- [Debug Squid-Cache Errors](https://raw.githubusercontent.com/maravento/blackweb/master/bwupdate/tools/debug_error.py)
- [Parse Domains](https://raw.githubusercontent.com/lsemel/python-parse-domain/master/tools/parse_domain.py) ([modified](https://raw.githubusercontent.com/maravento/blackweb/master/bwupdate/tools/parse_domain.py))
- [Debug internal lst](https://raw.githubusercontent.com/maravento/blackweb/master/bwupdate/tools/debuglst.sh)
- [CTFR](https://github.com/UnaPibaGeek/ctfr)
- [idn2](http://www.gnu.org/s/libidn/manual/html_node/Invoking-idn.html)
- [speedtest](https://raw.githubusercontent.com/sivel/speedtest-cli/master/speedtest.py) and [bandwidth](https://raw.githubusercontent.com/maravento/gateproxy/master/conf/scr/bandwidth.sh)

## BACKLINKS

---

- [OSINT Framework. *Domain Name/Domain Blacklists/Blackweb*](https://osintframework.com/)
- [Wikipedia. *Blacklist_(computing)*](https://en.wikipedia.org/wiki/Blacklist_(computing))
- [Zeltser. *Free Blocklists of Suspected Malicious IPs and URLs*](https://zeltser.com/malicious-ip-blocklists/)
- [Segu-Info. *Análisis de malware y sitios web en tiempo real*](https://blog.segu-info.com.ar/2019/07/analisis-de-malware-y-sitios-web-en.html)
- [covert.io. *Getting Started with DGA Domain Detection Research*](http://www.covert.io/getting-started-with-dga-research/)
- [Keystone Solutions. *blocklists*](https://keystonesolutions.io/solutions/blocklists/)
- [Secrepo. *Samples of Security Related Data*](http://www.secrepo.com/)
- [Soficas. *CiberSeguridad - Protección Activa*](https://soficas.com/noticias/proteccion-ciberseguridad.html)
- [Xploitlab. *Projects using WindowsSpyBlocker*](https://xploitlab.com/windowsspyblocker-block-spying-and-tracking-on-windows/)
- [Awesome Open Source. *Blackweb*](https://awesomeopensource.com/project/maravento/blackweb)
- [Lifars. *Sites with blocklist of malicious IPs and URLs*](https://lifars.com/wp-content/uploads/2017/06/LIFARS_Guide_Sites-with-blocklist-of-malicious-IPs-and-URLs.pdf)
- [Kerry Cordero. *Blocklists of Suspected Malicious IPs and URLs*](https://cordero.me/blocklists-of-suspected-malicious-ips-and-urls/)
- [stackoverflow.com. *Blacklist IP database*](https://stackoverflow.com/a/39516166/8747573)
- [opensourcelibs](https://opensourcelibs.com/lib/blackweb)

## CONTRIBUTIONS

---

We thank all those who have contributed to this project. Those interested can contribute, sending us links of new lists, to be included in this project / Agradecemos a todos aquellos que han contribuido a este proyecto. Los interesados pueden contribuir, enviándonos enlaces de nuevas listas, para ser incluidas en este proyecto

Special thanks to: [Jhonatan Sneider](https://github.com/sney2002)

## DONATE

---

BTC: 3M84UKpz8AwwPADiYGQjT9spPKCvbqm4Bc

## BUILD

---

[![CreativeCommons](https://licensebuttons.net/l/by-sa/4.0/88x31.png)](http://creativecommons.org/licenses/by-sa/4.0/)
[maravento.com](http://www.maravento.com) is licensed under a [Creative Commons Reconocimiento-CompartirIgual 4.0 Internacional License](http://creativecommons.org/licenses/by-sa/4.0/).

## OBJECTION

---

Due to recent arbitrary changes in computer terminology, it is necessary to clarify the meaning and connotation of the term **blacklist**, associated with this project: *In computing, a blacklist, denylist or blocklist is a basic access control mechanism that allows through all elements (email addresses, users, passwords, URLs, IP addresses, domain names, file hashes, etc.), except those explicitly mentioned. Those items on the list are denied access. The opposite is a whitelist, which means only items on the list are let through whatever gate is being used.*

Debido a los recientes cambios arbitrarios en la terminología informática, es necesario aclarar el significado y connotación del término **blacklist**, asociado a este proyecto: *En informática, una lista negra, lista de denegación o lista de bloqueo es un mecanismo básico de control de acceso que permite a través de todos los elementos (direcciones de correo electrónico, usuarios, contraseñas, URL, direcciones IP, nombres de dominio, hashes de archivos, etc.), excepto los mencionados explícitamente. Esos elementos en la lista tienen acceso denegado. Lo opuesto es una lista blanca, lo que significa que solo los elementos de la lista pueden pasar por cualquier puerta que se esté utilizando.*

Source [Wikipedia](https://en.wikipedia.org/wiki/Blacklist_(computing))

Therefore / Por tanto

**blacklist**, **blocklist**, **blackweb**, **blackip**, **whitelist**, **etc.**

are terms that have nothing to do with racial discrimination / son términos que no tienen ninguna relación con la discriminación racial

## NOTICE

---

The urls included in the acl `allowurls.txt` and` blockurls.txt`, may be notified to the admin, via email and will have a period of 72 hours to accept or reject the inclusion. After the deadline, the inclusion will be permanent, unless the object or url changes, or is included in a public block list / Las urls incluidas en las acl `allowurls.txt` y `blockurls.txt`, podrán ser notificadas al admin, via mail y tendrá un plazo de 72 horas para aceptar o rechazar la inclusión. Superado el plazo, la inclusión será permanente, excepto que cambie el objeto o url, o sea incluida en alguna lista de bloqueo pública

## DISCLAIMER

---

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
