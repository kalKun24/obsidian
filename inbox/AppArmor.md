# AppArmor
## 状態を確認する
``` bash
┌─[kal24hi@parrot]─[~]
└──╼ $sudo cat /sys/kernel/security/apparmor/profiles 
[sudo] kal24hi のパスワード:
smbldap-useradd (complain)
smbldap-useradd///etc/init.d/nscd (complain)
traceroute (complain)
smbd (complain)
/usr/sbin/ntpd (enforce)
nmbd (complain)
nscd (complain)
mdnsd (complain)
identd (complain)
dnsmasq (complain)
dnsmasq//libvirt_leaseshelper (complain)
/usr/sbin/haveged (enforce)
/usr/sbin/dhcpd (enforce)
/usr/sbin/cupsd (enforce)
/usr/sbin/cupsd//third_party (enforce)
/usr/lib/cups/backend/cups-pdf (enforce)
libreoffice-soffice (complain)
libreoffice-soffice//gpg (enforce)
/usr/sbin/cups-browsed (enforce)
avahi-daemon (complain)
apt-cacher-ng (enforce)
libreoffice-xpdfimport (enforce)
libreoffice-senddoc (enforce)
/usr/lib/ipsec/stroke (enforce)
libreoffice-oosplash (complain)
/usr/lib/ipsec/charon (enforce)
/usr/bin/totem-video-thumbnailer (enforce)
/usr/bin/totem-audio-preview (enforce)
/usr/bin/totem (enforce)
/usr/bin/totem//sanitized_helper (enforce)
/usr/bin/pidgin (enforce)
/usr/bin/pidgin//sanitized_helper (enforce)
tcpdump (enforce)
man_groff (enforce)
man_filter (enforce)
/usr/bin/man (enforce)
/usr/bin/irssi (complain)
torbrowser_tor (enforce)
torbrowser_firefox (enforce)
torbrowser_firefox//opencl_pocl_ld (enforce)
torbrowser_firefox//opencl_pocl_clang (enforce)
system_tor (enforce)
syslogd (complain)
syslog-ng (complain)
/{,usr/}sbin/dhclient (enforce)
/usr/lib/connman/scripts/dhclient-script (enforce)
/usr/lib/NetworkManager/nm-dhcp-helper (enforce)
/usr/lib/NetworkManager/nm-dhcp-client.action (enforce)
klogd (complain)
samba-rpcd-spoolss (complain)
samba-rpcd-classic (complain)
samba-rpcd (complain)
samba-dcerpcd (complain)
php-fpm (complain)
samba-bgqd (complain)
nvidia_modprobe (enforce)
nvidia_modprobe//kmod (enforce)
lsb_release (enforce)
/usr/lib/x86_64-linux-gnu/lightdm/lightdm-guest-session (enforce)
/usr/lib/x86_64-linux-gnu/lightdm/lightdm-guest-session//chromium (enforce)
ping (complain)

```

## 守られているプログラムを調べる
``` bash
┌─[kal24hi@parrot]─[~] 
└──╼ $sudo cat /sys/kernel/security/apparmor/profiles 
[sudo] kal24hi のパスワード:
smbldap-useradd (complain)
smbldap-useradd///etc/init.d/nscd (complain)
traceroute (complain)
smbd (complain)
.
(略)
.
samba-bgqd (complain)
nvidia_modprobe (enforce)
nvidia_modprobe//kmod (enforce)
lsb_release (enforce)
/usr/lib/x86_64-linux-gnu/lightdm/lightdm-guest-session (enforce)
/usr/lib/x86_64-linux-gnu/lightdm/lightdm-guest-session//chromium (enforce)
ping (complain)

```
### モード
- enforce(強制)
	- プロファイルで許可された動作のみを許可
- complain(学習)
	- プロファイルで許可されていない動作をログに記録(禁止はしない)

## プロファイル
### 置き場所
`/etc/apparmor.d`下にある
``` bash
┌─[kal24hi@parrot]─[~]
└──╼ $sudo ls /etc/apparmor.d/
abi		       local		samba-rpcd-classic	    torbrowser.Tor.tor	      usr.lib.ipsec.charon		       usr.sbin.cups-browsed  usr.sbin.nmbd
abstractions	       lsb_release	samba-rpcd-spoolss	    tunables		      usr.lib.ipsec.stroke		       usr.sbin.cupsd	      usr.sbin.nscd
apache2.d	       nvidia_modprobe	sbin.dhclient		    usr.bin.irssi	      usr.lib.libreoffice.program.oosplash     usr.sbin.dhcpd	      usr.sbin.ntpd
bin.ping	       php-fpm		sbin.klogd		    usr.bin.man		      usr.lib.libreoffice.program.senddoc      usr.sbin.dnsmasq       usr.sbin.smbd
dhcpd.d		       samba		sbin.syslog-ng		    usr.bin.pidgin	      usr.lib.libreoffice.program.soffice.bin  usr.sbin.haveged       usr.sbin.smbldap-useradd
disable		       samba-bgqd	sbin.syslogd		    usr.bin.tcpdump	      usr.lib.libreoffice.program.xpdfimport   usr.sbin.identd	      usr.sbin.traceroute
force-complain	       samba-dcerpcd	system_tor		    usr.bin.totem	      usr.sbin.apt-cacher-ng		       usr.sbin.mariadbd
lightdm-guest-session  samba-rpcd	torbrowser.Browser.firefox  usr.bin.totem-previewers  usr.sbin.avahi-daemon		       usr.sbin.mdnsd

```

### 無効化
manコマンドに対する例を紹介

#### 無効化されているプロファイルの検索

``` bash┌─[✗]─[kal24hi@parrot]─[~]
└──╼ $sudo ls -l /etc/apparmor.d/disable/
合計 0
```

現在のmanコマンドに対するプロファイルの確認
