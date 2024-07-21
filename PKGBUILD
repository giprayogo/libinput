# Maintainer: Andreas Radke <andyrtr@archlinux.org>

pkgname=libinput
pkgver=1.26.1
pkgrel=1.3
pkgdesc="Input device management and event handling library"
url="https://gitlab.freedesktop.org/libinput/libinput"
arch=(x86_64)
license=(MIT)
depends=('mtdev' 'libevdev' 'libwacom' 'systemd-libs' 'glibc')
# upstream doesn't recommend building docs
makedepends=('gtk4' 'meson' 'wayland-protocols' 'check') # 'doxygen' 'graphviz' 'python-sphinx' 'python-recommonmark'
checkdepends=('python-pytest')
optdepends=('gtk4: libinput debug-gui'
            'python-pyudev: libinput measure'
            'python-libevdev: libinput measure'
            'python-yaml: used by various tools')
source=(https://gitlab.freedesktop.org/libinput/libinput/-/archive/$pkgver/$pkgname-$pkgver.tar.bz2
        'smaller-hold-threshold.patch'
        'my-touchpad-profile.patch'
        'no-hysteresis.patch')
sha256sums=('da0ac450902a2aef29028bcab0bec26eb5e08b4c36ffc2925746d807794991b6'
            '2a099b397980bea5ddd07a84115ff2897c604a68185ac502b1de73a6ad0ee027'
            '52bcb376133c7b08a5c9d789e5f0f553d9c6c80db3e50460570a4baf80bcae47'
            '5d37a398fc729f08576f9f268fb9990f6ef73148c6143b3d00b436f57d413239')


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
  patch --directory=$pkgname-$pkgver --forward --strip=1 --input=../smaller-hold-threshold.patch
  patch --directory=$pkgname-$pkgver --forward --strip=1 --input=../my-touchpad-profile.patch
  patch --directory=$pkgname-$pkgver --forward --strip=1 --input=../no-hysteresis.patch
}

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