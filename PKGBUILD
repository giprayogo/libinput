# Maintainer: Andreas Radke <andyrtr@archlinux.org>
# Maintainer: Jan de Groot

pkgname=libinput
pkgver=1.8.2
pkgrel=1
pkgdesc="Input device management and event handling library"
url="https://www.freedesktop.org/wiki/Software/libinput/"
arch=(i686 x86_64)
license=(custom:X11)
depends=('mtdev' 'systemd' 'libevdev' 'libwacom')
makedepends=('doxygen' 'graphviz' 'gtk3' 'meson')
optdepends=('gtk3: libinput debug-gui')
source=(https://freedesktop.org/software/$pkgname/$pkgname-$pkgver.tar.xz{,.sig})
sha512sums=('555a7680cc8aaf62c5370a865f3aff0a933d42d94a3d8861c072666b02c9e1be45ea39de9a749a9575cdfb613b6150e412e18559d94d4919f21ca4680a3c76a7'
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
