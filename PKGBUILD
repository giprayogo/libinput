# Maintainer: Andreas Radke <andyrtr@archlinux.org>
# Maintainer: Jan de Groot

pkgname=libinput
pkgver=1.6.3
pkgrel=1
pkgdesc="Input device management and event handling library"
arch=(i686 x86_64)
url="https://www.freedesktop.org/wiki/Software/libinput/"
license=(custom:X11)
depends=('mtdev' 'systemd' 'libevdev' 'libwacom')
# currently no doc files to install
makedepends=('doxygen' 'graphviz' 'gtk3')
#checkdepends=('check' 'libunwind')
source=(https://freedesktop.org/software/$pkgname/$pkgname-$pkgver.tar.xz{,.sig})
sha256sums=('74da2798728e79c3aedfffa268d8fe811c3766ca3708309c0dc45502be137da1'
            'SKIP')
validpgpkeys=('3C2C43D9447D5938EF4551EBE23B7E70B467F0BF') # Peter Hutterer (Who-T) <office@who-t.net>

build() {
  cd $pkgname-$pkgver
  ./configure --prefix=/usr --disable-static
  make
}

check() {
  cd $pkgname-$pkgver
# disabled for now:
# https://github.com/libcheck/check/issues/18
#  make check
}

package() {
  cd $pkgname-$pkgver
  make DESTDIR="$pkgdir" install
  install -Dm644 COPYING "${pkgdir}/usr/share/licenses/${pkgname}/COPYING"
  # install doc - no Makefile target
  install -v -dm755 ${pkgdir}/usr/share/doc/libinput
  cp -rv doc/html/* ${pkgdir}/usr/share/doc/libinput
}
