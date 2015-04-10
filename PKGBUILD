# Maintainer: Andreas Radke <andyrtr@archlinux.org>
# Maintainer: Jan de Groot

pkgname=libinput
pkgver=0.13.0
pkgrel=2
pkgdesc="library that handles input devices for display servers and other applications that need to directly deal with input devices."
arch=(i686 x86_64)
url="http://www.freedesktop.org/wiki/Software/libinput/"
license=(custom:X11)
depends=('mtdev' 'libsystemd' 'libevdev')
makedepends=('systemd')
options=('!libtool')
source=(http://freedesktop.org/software/$pkgname/$pkgname-$pkgver.tar.xz{,.sig}
        fix_crash_for_missing_ABS_X_Y.diff)
sha256sums=('6cecaf7fde525f1d81474cbd495ce526d5e34c845d3e9d6f3e2565b7048cc61a'
            'SKIP'
            'c1d19d53f81ba0f98911917dd3239e9e52448f6d45d961e90dadbefb707316f9')
validpgpkeys=('3C2C43D9447D5938EF4551EBE23B7E70B467F0BF') # Peter Hutterer (Who-T) <office@who-t.net>

prepare() {
  cd $pkgname-$pkgver
  # https://bugs.freedesktop.org/show_bug.cgi?id=89783#c15 - FS#44416
  patch -Np1 -i ${srcdir}/fix_crash_for_missing_ABS_X_Y.diff
}

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
}
