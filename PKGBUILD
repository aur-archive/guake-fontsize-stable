# Maintainer: Ivan de Jesús Pompa García <ivan.pompa@gmx.com>

pkgname=guake-fontsize-stable
pkgver=0.4.4
pkgrel=2
pkgdesc="Drop-down terminal for GNOME with shortcuts for fontsize"
arch=('i686' 'x86_64')
url="http://projects.comum.org/guake"
license=('GPL')

depends=('python2-notify'
	'vte'
	'python2-gconf'
	'dbus-python')

makedepends=('intltool')

conflicts=('guake')
provides=('guake')

source=('http://guake.org/files/guake-0.4.4.tar.gz'
	'p-guake.patch'
	'p-prefs.py.patch'
	'p-guake.schemas.patch'
	'guake.install')

md5sums=('532adada29b8f0bb79dc15904aa6b70c'
	'210d753571a08f657def69ecfd3fa27a'
	'f90a2b3000cab3bddf620b0f519d0ffe'
	'ec71829fa4be268e5bdaab907f400bd9'
	'6231a937568f7c1f88c690791bd1742c')


build() {
	cp *.patch $srcdir/guake-$pkgver
	cd $srcdir/guake-$pkgver
	patch -Np1 < p-guake.patch
	patch -Np1 < p-prefs.py.patch
	patch -Np1 < p-guake.schemas.patch

	cd $srcdir/guake-$pkgver
	./configure --prefix=/usr --sysconfdir=/etc || return 1

	cd $srcdir/guake-$pkgver/po
	make update-po

	cd $srcdir/guake-$pkgver
	make
	make DESTDIR=$pkgdir install

	rm $pkgdir/usr/lib/python2.7/site-packages/guake/globalhotkeys.la
	rm $pkgdir/usr/lib/python2.7/site-packages/guake/globalhotkeys.a
	mkdir -p $pkgdir/usr/share/gconf/schemas
	mv $pkgdir/etc/gconf/schemas/guake.schemas \
	   $pkgdir/usr/share/gconf/schemas/guake.schemas
	rmdir $pkgdir/etc/gconf/schemas
	rmdir $pkgdir/etc/gconf
}

install=guake.install
