# Maintainer: Andreas Radke <andyrtr@archlinux.org>
# Maintainer: Jan de Groot

pkgname=libinput
pkgver=1.10.3
pkgrel=1
pkgdesc="Input device management and event handling library"
url="https://www.freedesktop.org/wiki/Software/libinput/"
arch=(x86_64)
license=(custom:X11)
depends=('mtdev' 'systemd' 'libevdev' 'libwacom')
makedepends=('doxygen' 'graphviz' 'gtk3' 'meson')
optdepends=('gtk3: libinput debug-gui'
            'python-pyudev: libinput measure'
            'python-evdev: libinput measure')
source=(https://freedesktop.org/software/$pkgname/$pkgname-$pkgver.tar.xz{,.sig})
sha512sums=('4c73673e138a7aff9d6f2d189b8afdfb51c868eca0487c8c487ffd3bb48849994a9095fbd4c5c725ee17fafc2a85298106e0cc7b59b4a8cd13ec28f65d15c01d'
            'SKIP')
validpgpkeys=('3C2C43D9447D5938EF4551EBE23B7E70B467F0BF') # Peter Hutterer (Who-T) <office@who-t.net>

prepare() {
  cd $pkgname-$pkgver
  # Reduce docs size
  printf '%s\n' >>doc/libinput.doxygen.in \
    HAVE_DOT=yes DOT_IMAGE_FORMAT=svg INTERACTIVE_SVG=yes
}

build() {
  arch-meson $pkgname-$pkgver build -Dtests=false
  ninja -C build
}

package() {
  DESTDIR="$pkgdir" ninja -C build install

  install -Dvm644 $pkgname-$pkgver/COPYING \
    "$pkgdir/usr/share/licenses/$pkgname/LICENSE"

  # install doc - no Makefile target
  install -d "$pkgdir/usr/share/doc"
  cp -av build/html "$pkgdir/usr/share/doc/libinput"
}
