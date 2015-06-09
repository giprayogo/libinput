# Maintainer: Andreas Radke <andyrtr@archlinux.org>
# Maintainer: Jan de Groot

pkgname=libinput
pkgver=0.17.0
pkgrel=2
pkgdesc="library that handles input devices for display servers and other applications that need to directly deal with input devices."
arch=(i686 x86_64)
url="http://www.freedesktop.org/wiki/Software/libinput/"
license=(custom:X11)
depends=('mtdev' 'systemd' 'libevdev')
install=libinput.install
options=('!libtool')
source=(http://freedesktop.org/software/$pkgname/$pkgname-$pkgver.tar.xz{,.sig}
        0001-filter-require-minimum-acceleration-factor-of-0.3.patch)
sha256sums=('b7db243be3a745c1031b364f3595ce9bb31347f874b7299ef8d44c98d2fb28db'
            'SKIP'
            '8d0fbee0669cdf6ad1318dcdb859efb59f6fb94d92e244fd71dd57a00fbda82b')
validpgpkeys=('3C2C43D9447D5938EF4551EBE23B7E70B467F0BF') # Peter Hutterer (Who-T) <office@who-t.net>

prepare() {
  cd $pkgname-$pkgver
  patch -Np1 -i ../0001-filter-require-minimum-acceleration-factor-of-0.3.patch
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
