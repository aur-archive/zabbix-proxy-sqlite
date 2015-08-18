# Maintainer: Karel Louwagie <karel@louwagie.net>
# Contributor: Idares <idares@seznam.cz>
# Contributor: Enrico Morelli <morelli@cerm.unifi.it>
# Contributor: Vadym Abramchuk <abramm@gmail.com>
# Contributor: karol_007 <karol.blazewicz@gmail.com>

pkgname=zabbix-proxy-sqlite
pkgver=2.4.5
pkgrel=1
pkgdesc="Software for monitoring of your applications, network and servers."
arch=('i686' 'x86_64' 'armv6h')
url="http://www.zabbix.com"
license=('GPL')
depends=('sqlite3' 'openipmi' 'libxml2')
backup=('etc/zabbix/zabbix_proxy.conf')

install='zabbix-proxy.install'
source=("http://downloads.sourceforge.net/project/zabbix/ZABBIX%20Latest%20Stable/$pkgver/zabbix-$pkgver.tar.gz"
        'zabbix-proxy.install'
	'zabbix-proxy.service'
	'zabbix-proxy.tmpfiles')

build() {
	cd $srcdir/zabbix-$pkgver
	./configure \
		--prefix=/usr \
		--sbindir=/usr/bin \
		--sysconfdir=/etc/zabbix \
		--enable-proxy \
		--enable-ipv6 \
		--with-sqlite3 \
		--with-ssh2 \
		--with-net-snmp \
		--with-openipmi \
		--with-libxml2 \
		--with-libcurl

	make
}

package() {
	cd $srcdir/zabbix-$pkgver
	make DESTDIR=$pkgdir install

	install -d -m0750 $pkgdir/var/log/zabbix

	install -D -m0644 $srcdir/zabbix-proxy.service $pkgdir/usr/lib/systemd/system/zabbix-proxy.service

	# change pid file location
	sed -i 's:# PidFile=.*:PidFile=/run/zabbix/zabbix_proxy.pid:' $pkgdir/etc/zabbix/zabbix_proxy.conf

	# tmpfile
	install -D -m 0644 $srcdir/zabbix-proxy.tmpfiles $pkgdir/usr/lib/tmpfiles.d/zabbix-proxy.conf
}

md5sums=('a82eb0d55d3ca947e10a4a55238f4388'
         '03a770db9cfaa2ae29f52035e6dbbf0f'
         '859debf8351561655532fcef05c28325'
         '9ce692356b4ac0a71595ce55fe3b44c1')
sha1sums=('4e5ed20341b7178a032fc131960eafd7683610f0'
          'ca05eedf61a31a6787e6282c5f80b856004cac78'
          '4f4c4d878bcd454d3859df6b5165ef792e087666'
          '8926befcb944732fd59a34c89b569d3fbef1ca9d')
sha512sums=('bdcba684b3d1cdb9eb5e1f9b370ef450201de8dbd9fe1619ef2b2437de6c34762dc041fa873976c4af0a2af229eec450aa58b1663feb75b6345d303484d35ead'
            '86dd58015364be82de75338439f2f2223e240513e2c5340201d0cb23976f7abb88fd53a2049c884380cd30a599e5d090732ea2cb6c52d2608bc3d6d7d8eb9f9e'
            '6e4e8f16e467afe472e958a3ca4246fd499d56c67544ee5b21fdf94cee698534f9bc3caedc49a207f652500e25d4251d6b708e098fa82858aeb385ab4fbba314'
            '3c63a2791e6ac77cb3144eb47a275cc8748f5c8943a076052300d6964994b95b18d60f504584fdcb683739dc514261402895e3f30ae2fbdb218acbc42c3d72df')
