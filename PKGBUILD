# This is an example PKGBUILD file. Use this as a start to creating your own,
# and remove these comments. For more information, see 'man PKGBUILD'.
# NOTE: Please fill out the license field for your package! If it is unknown,
# then please put 'unknown'.

# Maintainer: The Almighty Pegasus Epsilon <pegasus@pimpninjas.org>
pkgname=kmscon-patched-git
pkgver=8.21.g7b049ce
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
	git clone https://github.com/Aetf/kmscon.git . || \
	git pull
}

build() {
	test -f ./configure || NOCONFIGURE=1 ./autogen.sh
	./configure --prefix=/usr
	make
}

check() { make -k check; }
package() {
	make DESTDIR="$pkgdir/" install
	mkdir -p $pkgdir/usr/lib/systemd/system
	cp docs/kmsconvt@.service $pkgdir/usr/lib/systemd/system/kmsconvt@.service
}
pkgver() { git describe | sed -e 's/[^-]\+-//;s/-/./g'; }
