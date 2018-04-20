# $Id$
# Maintainer: Jan Alexander Steffens (heftig) <jan.steffens@gmail.com>

pkgname=libwacom-surface
pkgver=0.29
pkgrel=1
pkgdesc="Library to identify Wacom tablets and their features - patched for Surface devices"
arch=('x86_64')
url="https://github.com/linuxwacom/libwacom/wiki"
license=('MIT')
depends=('glib2' 'systemd' 'libgudev')
makedepends=('libxml2')
provides=('libwacom=0.29')
conflicts=('libwacom')
validpgpkeys=('3C2C43D9447D5938EF4551EBE23B7E70B467F0BF')
source=(
  "https://sourceforge.net/projects/linuxwacom/files/libwacom/libwacom-$pkgver.tar.bz2"{,.sig}
  'libwacom-surface.patch'
)
sha1sums=('6782d32af328bc984d7c4f65062f04a9172d342c'
          'SKIP'
          '9a38245dfbd7f85ce4e41b33a159b2c60c338e06')
sha256sums=('9cea00e68ddf342c3f749f6628d33fd3646f1937d7c57053ec6c5728d9a333b6'
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
