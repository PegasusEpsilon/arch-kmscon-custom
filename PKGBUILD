# Maintainer: The Almighty Pegasus Epsilon <pegasus@pimpninjas.org>
pkgname=arch-kmscon-custom
pkgver=8.40.g01dd0a2
pkgrel=1
pkgdesc="Linux KMS/DRM based virtual Console Emulator http://www.freedesktop.org/wiki/Software/kmscon"
url="https://github.com/dvdhrm/kmscon"
arch=('i686' 'x86_64')
license=('GPL')
depends=('libtsm')
provides=('kmscon')
conflicts=('kmscon' 'kmscon-git')
replaces=('kmscon' 'kmscon-git')

prepare() {
	# Most recent branch I can find.
	# Feel free to replace with one you like better.
	git clone https://github.com/CarlosNihelton/kmscon.git . || \
	git pull
# if it breaks, check out a working version.
#	git checkout 3f8b688221c059ae8945420d4b3fded288e13169 .
}

build() {
	test -f ./configure || NOCONFIGURE=1 ./autogen.sh
	./configure --prefix=/usr
	make
}

check() { make -k check; }

package() {
	make DESTDIR="$pkgdir/" install
	if [ -e /usr/lib/systemd ]; then
		mkdir -p $pkgdir/usr/lib/systemd/system
		cp docs/kmsconvt@.service $pkgdir/usr/lib/systemd/system/kmsconvt@.service
	else
		if [ -e /etc/init.d -a -e /etc/conf.d ]; then
			mkdir -p $pkgdir/etc/init.d
			cp ../kmscon $pkgdir/etc/init.d
			for i in 2 3 4 5 6; do
				ln -s kmscon $pkgdir/etc/init.d/kmscon.vt$i
			done
		fi
	fi
}

post_install() {
	libtool --finish /usr/lib/kmscon
}

pkgver() { git describe | sed -e 's/[^-]\+-//;s/-/./g'; }
