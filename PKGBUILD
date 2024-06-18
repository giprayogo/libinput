# Maintainer: Andreas Radke <andyrtr@archlinux.org>

pkgname=libinput
pkgver=1.25.0
pkgrel=1.10
pkgdesc="Input device management and event handling library"
url="https://wayland.freedesktop.org/libinput/doc/$pkgver/"
arch=(x86_64)
license=(MIT)
depends=('mtdev' 'systemd' 'libevdev' 'libwacom' 'systemd-libs' 'glibc')
# upstream doesn't recommend building docs
makedepends=('gtk4' 'meson' 'wayland-protocols' 'check') # 'doxygen' 'graphviz' 'python-sphinx' 'python-recommonmark'
checkdepends=('python-pytest')
optdepends=('gtk4: libinput debug-gui'
  'python-pyudev: libinput measure'
  'python-libevdev: libinput measure'
  'python-yaml: used by various tools')
source=(https://gitlab.freedesktop.org/libinput/libinput/-/archive/$pkgver/$pkgname-$pkgver.tar.bz2
  'smaller-hold-threshold.patch' 'my-touchpad-profile.patch')
sha256sums=('193bd592298bd9e369c0ef3e5d83a6a9d68ddc4cd3dfc84bbe77920a8d0d57df'
            '51989b148b71f84ecbb1e771f2b4543391bd91e4acf5213e8799adb85ee97379'
            '7531666484de13c9b4eb8132bf0facfb137317a035831aecaf95e203f829f394')

#validpgpkeys=('3C2C43D9447D5938EF4551EBE23B7E70B467F0BF') # Peter Hutterer (Who-T) <office@who-t.net>

build() {
  arch-meson $pkgname-$pkgver build \
    -D udev-dir=/usr/lib/udev \
    -D documentation=false

  # Print config
  meson configure build

  meson compile -C build
}

check() {
  meson test -C build --print-errorlogs
}

package() {
  meson install -C build --destdir "$pkgdir"

  install -Dvm644 $pkgname-$pkgver/COPYING \
    "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

prepare() {
  patch --directory=$pkgname-$pkgver --forward --strip=1 --input=../no-hysteresis.patch
}
