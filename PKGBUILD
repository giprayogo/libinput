# Maintainer: Andreas Radke <andyrtr@archlinux.org>
# Maintainer: Jan de Groot

pkgname=libinput
pkgver=1.2.3
pkgrel=1
pkgdesc="library that handles input devices for display servers and other applications that need to directly deal with input devices."
arch=(i686 x86_64)
url="http://www.freedesktop.org/wiki/Software/libinput/"
license=(custom:X11)
depends=('mtdev' 'systemd' 'libevdev' 'libwacom')
checkdepends=('check')
install=libinput.install
options=('!libtool')
source=(http://freedesktop.org/software/$pkgname/$pkgname-$pkgver.tar.xz{,.sig})
sha256sums=('09b2a9d3a0cc973a9d3fdc7af40162cbef0b16be0a2e415786f83761f519e9f2'
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
}
