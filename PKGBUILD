# Maintainer: Antonio Rojas <nqn76sw@gmail.com>

pkgname=palp
pkgver=2.1
pkgrel=1
pkgdesc="A Package for analyzing Lattice Polytopes"
arch=('i686' 'x86_64')
url="http://hep.itp.tuwien.ac.at/~kreuzer/CY/CYpalp.html"
license=('GPL3')
depends=()
source=("http://hep.itp.tuwien.ac.at/~kreuzer/CY/$pkgname/$pkgname-$pkgver.tar.gz")
md5sums=('f3791acd2e60846cb63bc98e87ad7509')

build() {
  cd $pkgname-$pkgver
  mkdir bin
  mv Global.h Global.h-template
  for dim in 4 5 6 11; do
    sed "s/^#define[^a-zA-Z]*POLY_Dmax.*/#define POLY_Dmax $dim/" Global.h-template > Global.h
    make
    for file in poly class cws nef mori; do
        mv ${file}.x bin/${file}-${dim}d.x
    done
  done
}

package() {
  cd $pkgname-$pkgver
  mkdir -p "$pkgdir"/usr/bin
  pushd bin
    for exe in *.x; do
	install -m 755 $exe "$pkgdir"/usr/bin
    done
  popd
  for file in poly class cws nef mori; do
    ln -sf ${file}-6d.x "$pkgdir"/usr/bin/${file}.x
  done
}

