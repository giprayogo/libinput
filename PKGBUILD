# Maintainer: Andreas Radke <andyrtr@archlinux.org>
# Maintainer: Jan de Groot

pkgname=libinput
pkgver=1.7.902
pkgrel=1
pkgdesc="Input device management and event handling library"
url="https://www.freedesktop.org/wiki/Software/libinput/"
arch=(i686 x86_64)
license=(custom:X11)
depends=('mtdev' 'systemd' 'libevdev' 'libwacom')
makedepends=('doxygen' 'graphviz' 'gtk3' 'meson')
source=(https://freedesktop.org/software/$pkgname/$pkgname-$pkgver.tar.xz{,.sig})
sha512sums=('022caa34e110e59d64bc2b06eaf50441c66c5fc44685c66923f5688cf1001da980cea991b7f6f348296446ba08f67c9697caef0a938bb59e6054aa7b2c5b0bbe'
            'SKIP')
validpgpkeys=('3C2C43D9447D5938EF4551EBE23B7E70B467F0BF') # Peter Hutterer (Who-T) <office@who-t.net>

prepare() {
  mkdir build
  cd $pkgname-$pkgver
}

build() {
  cd build
  meson --prefix=/usr --buildtype=release ../$pkgname-$pkgver --libexecdir=/usr/lib \
    -Dtests=false
  ninja
}

package() {
  cd build
  DESTDIR="$pkgdir" ninja install

  cd ../$pkgname-$pkgver
  install -Dvm644 COPYING "$pkgdir/usr/share/licenses/$pkgname/LICENSE"

  # install doc - no Makefile target
  install -dv "$pkgdir/usr/share/doc/libinput"
  cp -av doc/html/* "$pkgdir/usr/share/doc/libinput"
}
