# $Id$
# Maintainer: Jan Alexander Steffens (heftig) <jan.steffens@gmail.com>

pkgname=libwacom-surface
pkgver=0.32
pkgrel=1
pkgdesc="Library to identify Wacom tablets and their features - patched for Surface devices"
arch=('x86_64')
url="https://github.com/linuxwacom/libwacom/wiki"
license=('MIT')
depends=('glib2' 'systemd' 'libgudev')
makedepends=('libxml2')
provides=('libwacom=0.31')
conflicts=('libwacom')
validpgpkeys=('3C2C43D9447D5938EF4551EBE23B7E70B467F0BF')
source=(
  https://github.com/linuxwacom/libwacom/releases/download/libwacom-${pkgver}/libwacom-${pkgver}.tar.bz2{,.sig}
  'libwacom-surface.patch'
)
sha1sums=('6fff41ed99a5f36714a55aba9268e87db851ab0e'
          'SKIP'
          '9a38245dfbd7f85ce4e41b33a159b2c60c338e06')
sha256sums=('6b9dab8bce0471b839c89d34a1b30839de2c24db03796fa8d572817830f85380'
            'SKIP'
            'c3ffa52b6b66e281342e87a6bcf7f8c4c4bbf1566b5fb4bfac87e09218695034')

prepare() {
  cd libwacom-$pkgver
  patch -p1 -i ../libwacom-surface.patch
}

build() {
  cd libwacom-$pkgver
  ./configure --prefix=/usr
  make
}

check() {
  cd libwacom-$pkgver
  make check
}

package() {
  cd libwacom-$pkgver
  make DESTDIR="$pkgdir" install
  install -D -m644 COPYING "${pkgdir}/usr/share/licenses/libwacom/LICENSE"
  install -m755 -d ${pkgdir}/usr/lib/udev/rules.d
  cd tools
  ./generate-udev-rules > ${pkgdir}/usr/lib/udev/rules.d/65-libwacom.rules
  
}
