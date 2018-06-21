# Maintainer: Andreas Radke <andyrtr@archlinux.org>
# Maintainer: Jan de Groot

pkgname=libinput
pkgver=1.11.1
pkgrel=2
pkgdesc="Input device management and event handling library"
url="https://www.freedesktop.org/wiki/Software/libinput/"
arch=(x86_64)
license=(custom:X11)
depends=('mtdev' 'systemd' 'libevdev' 'libwacom')
makedepends=('doxygen' 'graphviz' 'gtk3' 'meson')
optdepends=('gtk3: libinput debug-gui'
            'python-pyudev: libinput measure'
            'python-evdev: libinput measure')
source=(https://freedesktop.org/software/$pkgname/$pkgname-$pkgver.tar.xz{,.sig}
        pass_a_valid_grab_parameter_to_list-devices.patch)
sha512sums=('3dd1a318c89d66f5a66016c6dbfa5277b61a8cb5337d99f85b1eeef40ed894bdc04fd4588a97383988daea0f034df5a72bff318325320a01b857db9deb94a2b0'
            'SKIP'
            '98ced6bcc5bc0ae22fbf2c9fe74bffb79eb575f34f0e0dfb8c7b84b3e54aee94b0bfb9ba0245b19a920e4d01984f7fc26029bbb7963cbce03409ea8db2dc9d7c')
validpgpkeys=('3C2C43D9447D5938EF4551EBE23B7E70B467F0BF') # Peter Hutterer (Who-T) <office@who-t.net>

prepare() {
  cd $pkgname-$pkgver
  # fix core dump in list-devices FS#59082
  patch -Np1 -i ../pass_a_valid_grab_parameter_to_list-devices.patch
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
