# chroot-containing-debian
Utils &amp; config to make creating a debian chroot quick &amp; painless

## Steps
* Create your chroot vm
```
apt-get install debootstrap git rsync
mkdir -p /opt/jail/{jessie,devel}
debootstrap jessie /opt/jail/jessie http://cdn.debian.org/debian
rsync -avPW /opt/jail/{jessie,devel}/
echo devel >/opt/jail/devel/etc/debian_chroot
```

* Clone this repo
```
cd /opt/jail/devel
git clone --depth 1 https://github.com/niczero/chroot-containing-debian.git root/build
```

* Install helpers on the host
```
cp -p root/build/usr/local/sbin/*mount_jail /usr/local/sbin/
```

* Mount the jail
```
mount_jail devel
chroot /opt/jail/devel
```

* Run initial setup
```
dpkg-reconfigure debconf
/root/build/root/bin/chroot_set_up
apt-get install locales
```
