# $Id$
# Maintainer: Jan Alexander Steffens (heftig) <jan.steffens@gmail.com>

pkgname=libwacom-surface
pkgver=0.27
pkgrel=1
pkgdesc="Library to identify Wacom tablets and their features - patched for Surface devices"
arch=('x86_64')
url="http://linuxwacom.sourceforge.net/wiki/index.php/Libwacom"
license=('MIT')
depends=('glib2' 'systemd' 'libgudev')
provides=('libwacom=0.27')
conflicts=('libwacom')
validpgpkeys=('3C2C43D9447D5938EF4551EBE23B7E70B467F0BF')
source=(
  "https://sourceforge.net/projects/linuxwacom/files/libwacom/libwacom-$pkgver.tar.bz2"{,.sig}
  'libwacom-surface.patch'
)
sha1sums=('681010a17a3a12eda0226778ab8adba9ed6a7708'
          'SKIP'
          '9a38245dfbd7f85ce4e41b33a159b2c60c338e06')
sha256sums=('f340d0010cc5dece8e4523b1e3220a98cba7939450ddbc017e86a134ceaece14'
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
  cd $pkgname-$pkgver
  make check
}

package() {
  cd $pkgname-$pkgver
  make DESTDIR="$pkgdir" install
  install -D -m644 COPYING "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
  install -m755 -d ${pkgdir}/usr/lib/udev/rules.d
  cd tools
  ./generate-udev-rules > ${pkgdir}/usr/lib/udev/rules.d/65-libwacom.rules
  
}
