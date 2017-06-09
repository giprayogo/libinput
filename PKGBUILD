# Maintainer: Andreas Radke <andyrtr@archlinux.org>
# Maintainer: Jan de Groot

pkgname=libinput
pkgver=1.7.3
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
sha512sums=('2262dc56d213a4d3ea765e870af200e2c336a166baa1bbdf5205e3ce70faefc777429ba09563c5dd79feb5442f53abc84e04a0f32a06bb622d6e120bb8ad152b'
            'SKIP')
validpgpkeys=('3C2C43D9447D5938EF4551EBE23B7E70B467F0BF') # Peter Hutterer (Who-T) <office@who-t.net>

build() {
  cd $pkgname-$pkgver
  ./configure --prefix=/usr --disable-static
  make
}

check() {
  cd $pkgname-$pkgver
  make check
}

package() {
  cd $pkgname-$pkgver
  make DESTDIR="$pkgdir" install
  install -Dm644 COPYING "${pkgdir}/usr/share/licenses/${pkgname}/COPYING"
  # install doc - no Makefile target
  install -v -dm755 ${pkgdir}/usr/share/doc/libinput
  cp -rv doc/html/* ${pkgdir}/usr/share/doc/libinput
}
