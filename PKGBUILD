# Contributor: Dale Blount <dale@archlinux.org>
# Contributor: Gregor Ibic <gregor.ibic@intelicom.si>
# Contributor: Gaetan Bisson <bisson@archlinux.org>
# Maintainer: xjpvictor Huang <ke AT xjpvictor dot info>

pkgname=clamav-milter
_pkgname=clamav
pkgver=0.98.5
pkgrel=1
pkgdesc='Anti-virus toolkit for Unix with libmilter built in'
url='http://www.clamav.net/'
license=('GPL')
options=('!libtool')
arch=('i686' 'x86_64')
depends=('bzip2' 'libltdl')
makedepends=('libmilter')
conflicts=('clamav')
backup=('etc/clamav/clamd.conf'
        'etc/clamav/freshclam.conf'
        'etc/clamav/clamav-milter.conf')
source=("http://downloads.sourceforge.net/project/${_pkgname}/${_pkgname}/${pkgver}/${_pkgname}-${pkgver}.tar.gz"
        'service'
        'service.fresh'
        'service.milter'
        'logrotate'
        'tmpfiles.d'
        'config.patch')

install=install

prepare() {
	cd "${srcdir}/${_pkgname}-${pkgver}"
	patch -p1 -i ../config.patch
}

build() {
	cd "${srcdir}/${_pkgname}-${pkgver}"
	./configure \
		--prefix=/usr \
		--sbindir=/usr/bin \
		--sysconfdir=/etc/clamav \
		--with-dbdir=/var/lib/clamav \
		--disable-clamav \
                --enable-milter \

	make
}

package() {
	cd "${srcdir}/${_pkgname}-${pkgver}"
	make DESTDIR="${pkgdir}" install

        install -Dm644 ./etc/clamd.conf.sample "${pkgdir}"/etc/clamav/clamd.conf
        install -Dm644 ./etc/freshclam.conf.sample "${pkgdir}"/etc/clamav/freshclam.conf
        install -Dm644 ./etc/clamav-milter.conf.sample "${pkgdir}"/etc/clamav/clamav-milter.conf
	install -Dm644 ../service.milter "${pkgdir}"/usr/lib/systemd/system/clamav-milter.service
	install -Dm644 ../service.fresh "${pkgdir}"/usr/lib/systemd/system/freshclamd.service
	install -Dm644 ../service "${pkgdir}"/usr/lib/systemd/system/clamd.service
	install -Dm644 ../tmpfiles.d "${pkgdir}"/usr/lib/tmpfiles.d/clamav.conf
	install -Dm644 ../logrotate "${pkgdir}"/etc/logrotate.d/clamav

	install -d -o 64 -g 64 "${pkgdir}"/run/clamav
	install -d -o 64 -g 64 "${pkgdir}"/var/log/clamav
	install -d -o 64 -g 64 "${pkgdir}"/var/lib/clamav
}
md5sums=('abb5c7efaff3394c0a49ff970841a2ac'
         'ea0beeef854b4a3cf6b25dc49b228f56'
         '5aecdce847da3872927b6a44f11cbbbb'
         '25c6ce07c4f958cbdda85a258cfcd6c1'
         'adc77ffacde04583acae8c55eb07bc48'
         '89ed33d37ca79d45b8c02418df2486e6'
         '199e058bb903c77155ecb96c157d73a3')
