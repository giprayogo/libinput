# Maintainer: Andreas Radke <andyrtr@archlinux.org>
# Maintainer: Jan de Groot

pkgname=libinput
pkgver=1.10.0+25+g3e77f2e9
pkgrel=1
pkgdesc="Input device management and event handling library"
url="https://www.freedesktop.org/wiki/Software/libinput/"
arch=(x86_64)
license=(custom:X11)
depends=('mtdev' 'systemd' 'libevdev' 'libwacom')
makedepends=('doxygen' 'graphviz' 'gtk3' 'meson' git)
optdepends=('gtk3: libinput debug-gui'
            'python-pyudev: libinput measure'
            'python-evdev: libinput measure')
_commit=3e77f2e9f5a98fc5917642bd47ceeef89b95c858  # master
source=("git+https://anongit.freedesktop.org/git/wayland/libinput#commit=$_commit")
sha512sums=('SKIP')

pkgver() {
  cd $pkgname
  git describe --tags | sed 's/-/+/g'
}

prepare() {
  cd $pkgname
  # Reduce docs size
  printf '%s\n' >>doc/libinput.doxygen.in \
    HAVE_DOT=yes DOT_IMAGE_FORMAT=svg INTERACTIVE_SVG=yes
}

build() {
  arch-meson $pkgname build -Dtests=false
  ninja -C build
}

package() {
  DESTDIR="$pkgdir" ninja -C build install

  install -Dvm644 $pkgname/COPYING \
    "$pkgdir/usr/share/licenses/$pkgname/LICENSE"

  # install doc - no Makefile target
  install -d "$pkgdir/usr/share/doc"
  cp -av build/html "$pkgdir/usr/share/doc/libinput"
}
