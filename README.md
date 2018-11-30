# lxd-image-xenial-light
###### Light image with Ubuntu Xenial for use with lxc/lxd

## Import
* Download [xenial-light2.tar.gz](https://github.com/cryptofuture/lxd-image-xenial-light/raw/master/xenial-light2.tar.gz)
* Check sha256sum with `sha256sum xenial-light2.tar.gz`

```bash
# Correct output:
22109ae09b16ed2c786757bb469fae96a789c466c15b6128f4228cff111710aa  xenial-light2.tar.gz
```

* Import image with: `lxc image import xenial-light2.tar.gz --alias xenial-light2`

## Create container from image
* Run `lxc launch xenial-light2 containernameyouwish`

## About image and extra installed software
Image is a lot like only base system, but with some extra soft installed. You can remove it, if you don't like. Less then 300Mb compressed, and less then 700Mb as a container.
### Extra software installed
htop, mc, duply, duplicity and unattended-upgrades. Also systemd-cron installed instead default cron, you need to add user to cron group, if you need to run cron jobs with user.
### Modifications made
`txqueuelen 10000 for eth0` in `/etc/network/interfaces`

```bash
# Base sources.list
deb http://us.archive.ubuntu.com/ubuntu/ xenial main restricted universe multiverse
deb-src http://us.archive.ubuntu.com/ubuntu/ xenial main restricted universe multiverse
deb http://security.ubuntu.com/ubuntu/ xenial-security main restricted universe multiverse
deb-src http://security.ubuntu.com/ubuntu/ xenial-security main restricted universe multiverse
deb http://us.archive.ubuntu.com/ubuntu/ xenial-updates main restricted universe multiverse
deb-src http://us.archive.ubuntu.com/ubuntu/ xenial-updates main restricted universe multiverse
deb http://us.archive.ubuntu.com/ubuntu/ xenial-backports main restricted universe multiverse
deb-src http://us.archive.ubuntu.com/ubuntu/ xenial-backports main restricted universe multiverse
deb http://archive.ubuntu.com/ubuntu/ xenial-proposed main restricted universe multiverse
deb-src http://archive.ubuntu.com/ubuntu/ xenial-proposed main restricted universe multiverse
# In /etc/apt/sources.list.d/hda-me-ubuntu-*
deb http://ppa.launchpad.net/hda-me/duply/ubuntu xenial main
deb http://ppa.launchpad.net/hda-me/proxychains-ng/ubuntu xenial main
# In /etc/apt/sources.list.d/saltstack.list
deb http://repo.saltstack.com/apt/ubuntu/16.04/amd64/latest xenial main
```

```bash
# Unattended-Upgrades activated and changed
Unattended-Upgrade::Allowed-Origins {
    "${distro_id}:${distro_codename}-security";
    "${distro_id}:${distro_codename}-updates";
    "${distro_id}:${distro_codename}-proposed";
//	"${distro_id}:${distro_codename}-backports";
    "LP-PPA-hda-me-duply:${distro_codename}";
    "LP-PPA-hda-me-proxychains-ng:${distro_codename}";
    "SaltStack:"
};
```

```bash
# Software recommends disabled in 99synaptic file
APT::Install-Recommends "false";
```

`/etc/update-manager/release-upgrades` changed to `Prompt=never`, [very cpu intensive](https://askubuntu.com/questions/322343/check-new-release-process-eating-up-resources-on-ubuntu-server-13-04)  

## List of packages

```sh
# dpkg --get-selections | grep -v deinstall output:
acl						install
adduser						install
apparmor					install
apt						install
apt-transport-https				install
apt-utils					install
base-files					install
base-passwd					install
bash						install
bash-completion					install
bind9-host					install
bsdmainutils					install
bsdutils					install
btrfs-tools					install
busybox-initramfs				install
busybox-static					install
bzip2						install
ca-certificates					install
command-not-found				install
command-not-found-data				install
coreutils					install
cpio						install
curl						install
dash						install
debconf						install
debconf-i18n					install
debianutils					install
dh-python					install
diffutils					install
distro-info-data				install
dmidecode					install
dmsetup						install
dnsmasq-base					install
dnsutils					install
dosfstools					install
dpkg						install
duplicity					install
duply						install
e2fslibs:amd64					install
e2fsprogs					install
ed						install
eject						install
file						install
findutils					install
friendly-recovery				install
ftp						install
fuse						install
gcc-5-base:amd64				install
gcc-6-base:amd64				install
geoip-database					install
gettext-base					install
gir1.2-glib-2.0:amd64				install
git						install
git-man						install
gnupg						install
gpgv						install
grep						install
groff-base					install
gzip						install
hdparm						install
hostname					install
htop						install
ifupdown					install
info						install
init						install
init-system-helpers				install
initramfs-tools					install
initramfs-tools-bin				install
initramfs-tools-core				install
initscripts					install
insserv						install
install-info					install
iproute2					install
iptables					install
iputils-ping					install
iputils-tracepath				install
isc-dhcp-client					install
isc-dhcp-common					install
iso-codes					install
keyboard-configuration				install
klibc-utils					install
kmod						install
krb5-locales					install
less						install
libaccountsservice0:amd64			install
libacl1:amd64					install
libapparmor-perl				install
libapparmor1:amd64				install
libapt-inst2.0:amd64				install
libapt-pkg5.0:amd64				install
libasn1-8-heimdal:amd64				install
libasprintf0v5:amd64				install
libattr1:amd64					install
libaudit-common					install
libaudit1:amd64					install
libbind9-140:amd64				install
libblkid1:amd64					install
libbsd0:amd64					install
libbz2-1.0:amd64				install
libc-bin					install
libc6:amd64					install
libcap-ng0:amd64				install
libcap2:amd64					install
libcap2-bin					install
libcomerr2:amd64				install
libcryptsetup4:amd64				install
libcurl3-gnutls:amd64				install
libdb5.3:amd64					install
libdbus-1-3:amd64				install
libdbus-glib-1-2:amd64				install
libdebconfclient0:amd64				install
libdevmapper1.02.1:amd64			install
libdns-export162				install
libdns162:amd64					install
libdrm2:amd64					install
libedit2:amd64					install
libelf1:amd64					install
liberror-perl					install
libestr0					install
libexpat1:amd64					install
libfdisk1:amd64					install
libffi6:amd64					install
libfribidi0:amd64				install
libfuse2:amd64					install
libgcc1:amd64					install
libgcrypt20:amd64				install
libgdbm3:amd64					install
libgeoip1:amd64					install
libgirepository-1.0-1:amd64			install
libglib2.0-0:amd64				install
libglib2.0-data					install
libgmp10:amd64					install
libgnutls-openssl27:amd64			install
libgnutls30:amd64				install
libgpg-error0:amd64				install
libgpm2:amd64					install
libgssapi-krb5-2:amd64				install
libgssapi3-heimdal:amd64			install
libhcrypto4-heimdal:amd64			install
libheimbase1-heimdal:amd64			install
libheimntlm0-heimdal:amd64			install
libhogweed4:amd64				install
libhx509-5-heimdal:amd64			install
libicu55:amd64					install
libidn11:amd64					install
libisc-export160				install
libisc160:amd64					install
libisccc140:amd64				install
libisccfg140:amd64				install
libjson-c2:amd64				install
libk5crypto3:amd64				install
libkeyutils1:amd64				install
libklibc					install
libkmod2:amd64					install
libkrb5-26-heimdal:amd64			install
libkrb5-3:amd64					install
libkrb5support0:amd64				install
libldap-2.4-2:amd64				install
liblocale-gettext-perl				install
liblwres141:amd64				install
liblxc1						install
liblz4-1:amd64					install
liblzma5:amd64					install
liblzo2-2:amd64					install
libmagic1:amd64					install
libmnl0:amd64					install
libmount1:amd64					install
libmpdec2:amd64					install
libmpfr4:amd64					install
libncurses5:amd64				install
libncursesw5:amd64				install
libnetfilter-conntrack3:amd64			install
libnettle6:amd64				install
libnewt0.52:amd64				install
libnfnetlink0:amd64				install
libnih1:amd64					install
libnuma1:amd64					install
libp11-kit0:amd64				install
libpam-modules:amd64				install
libpam-modules-bin				install
libpam-runtime					install
libpam0g:amd64					install
libparted2:amd64				install
libpcap0.8:amd64				install
libpci3:amd64					install
libpcre3:amd64					install
libperl5.22:amd64				install
libpipeline1:amd64				install
libplymouth4:amd64				install
libpng12-0:amd64				install
libpopt0:amd64					install
libprocps4:amd64				install
libpython-stdlib:amd64				install
libpython2.7-minimal:amd64			install
libpython2.7-stdlib:amd64			install
libpython3-stdlib:amd64				install
libpython3.5-minimal:amd64			install
libpython3.5-stdlib:amd64			install
libreadline6:amd64				install
libroken18-heimdal:amd64			install
librsync1:amd64					install
librtmp1:amd64					install
libsasl2-2:amd64				install
libsasl2-modules:amd64				install
libsasl2-modules-db:amd64			install
libseccomp2:amd64				install
libselinux1:amd64				install
libsemanage-common				install
libsemanage1:amd64				install
libsepol1:amd64					install
libsigsegv2:amd64				install
libslang2:amd64					install
libsmartcols1:amd64				install
libsqlite3-0:amd64				install
libss2:amd64					install
libssh2-1:amd64					install
libssl1.0.0:amd64				install
libstdc++6:amd64				install
libsystemd0:amd64				install
libtasn1-6:amd64				install
libtext-charwidth-perl				install
libtext-iconv-perl				install
libtext-wrapi18n-perl				install
libtinfo5:amd64					install
libudev1:amd64					install
libusb-0.1-4:amd64				install
libusb-1.0-0:amd64				install
libustr-1.0-1:amd64				install
libuuid1:amd64					install
libwind0-heimdal:amd64				install
libwrap0:amd64					install
libx11-6:amd64					install
libx11-data					install
libxau6:amd64					install
libxcb1:amd64					install
libxdmcp6:amd64					install
libxext6:amd64					install
libxml2:amd64					install
libxmuu1:amd64					install
libxtables11:amd64				install
libyaml-0-2:amd64				install
linux-base					install
locales						install
login						install
logrotate					install
lsb-base					install
lsb-release					install
lshw						install
lsof						install
ltrace						install
lxc-common					install
lxcfs						install
lxd						install
lxd-client					install
makedev						install
man-db						install
manpages					install
mawk						install
mc						install
mc-data						install
mime-support					install
mlocate						install
mount						install
mtr-tiny					install
multiarch-support				install
ncurses-base					install
ncurses-bin					install
net-tools					install
netbase						install
netcat-openbsd					install
openssh-client					install
openssh-sftp-server				install
openssl						install
parted						install
passwd						install
patch						install
pciutils					install
perl						install
perl-base					install
perl-modules-5.22				install
popularity-contest				install
powermgmt-base					install
procps						install
proxychains-ng					install
psmisc						install
python						install
python-apt-common				install
python-lockfile					install
python-minimal					install
python2.7					install
python2.7-minimal				install
python3						install
python3-apt					install
python3-commandnotfound				install
python3-dbus					install
python3-distupgrade				install
python3-gdbm:amd64				install
python3-gi					install
python3-minimal					install
python3-pkg-resources				install
python3-pycurl					install
python3-software-properties			install
python3-update-manager				install
python3.5					install
python3.5-minimal				install
readline-common					install
resolvconf					install
rsync						install
rsyslog						install
sed						install
sensible-utils					install
sgml-base					install
shared-mime-info				install
software-properties-common			install
squashfs-tools					install
strace						install
sudo						install
systemd						install
systemd-cron					install
systemd-sysv					install
sysv-rc						install
sysvinit-utils					install
tar						install
tcpdump						install
time						install
tzdata						install
ubuntu-keyring					install
ubuntu-release-upgrader-core			install
ucf						install
udev						install
uidmap						install
unattended-upgrades				install
unzip						install
update-manager-core				install
usbutils					install
util-linux					install
uuid-runtime					install
wget						install
whiptail					install
xauth						install
xkb-data					install
xml-core					install
xz-utils					install
zlib1g:amd64					install
```
## Donation

Consider making a donation, if you like what I doing.
I working remotely and income is unstable, so every little bit helps.

Also it would be nice if you provide, a note on `admin@hda.me` after making a donation with information what you like and what you want to improve. So, I would consider giving more time and support to particular project.

I also open to reasonable work offers, especially if offer would be close to a field or project I work with.

### E-money & Fiat

#### Yandex Money
Donation on Yandex Money: https://money.yandex.ru/to/410015241627045)
#### Advanced Cash
Open https://wallet.advcash.com/pages/transfer/wallet and use `mmail@sent.com` in `Specify the recipient's wallet or e-mail` field
#### PayPal
Donation with PayPal: https://paypal.me/hdadonation
#### Payeer
Donation with Payeer: On https://payeer.com/en/account/send/ use `P2865115` in `Account, e-mail or phone number` field

### Cryptocurrency

#### Bitcoin
Address is `1N5czHaoSLukFSTq2ZJujaWGjkmBxv2dT9`
#### Musicoin
Address is `0xf449f8c17a056e9bfbefe39637c38806246cb2c9`
#### Ethereum
Address is `0x23459a89eAc054bdAC1c13eB5cCb39F42574C26a`
#### Other
I could provide you with some relatively cheap "hardware" donation options directly to my PO Box, if you prefer real gifts. Ask for details on `admin@hda.me`
