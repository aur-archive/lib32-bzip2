# Maintainer: TryA <tryagainprod {at} gmail.com>
# Contributor: Judd <jvinet@zeroflux.org> 

_pkgbasename=bzip2
pkgname=lib32-bzip2
pkgver=1.0.6
pkgrel=1
pkgdesc="A high-quality data compression program (32-bit)"
arch=('x86_64')
license=('custom')
url="http://sources.redhat.com/bzip2"
depends=('lib32-glibc' $_pkgbasename)
makedepends=('gcc-multilib')
source=(http://www.bzip.org/$pkgver/bzip2-$pkgver.tar.gz)
md5sums=('00b516f4704d4a7cb50a1d97e6e8e15b')

build() {
  cd ${srcdir}/${_pkgbasename}-${pkgver}

  sed -i "s|CC=gcc|CC=gcc -m32|" Makefile
  sed -i "s|CC=gcc|CC=gcc -m32|" Makefile-libbz2_so
  
  # add large-file support
  sed -e 's/^CFLAGS=\(.*\)$/CFLAGS=\1 \$(BIGFILES)/' -i ./Makefile-libbz2_so
  
  # use our optimization
  sed -i "s|-O2|${CFLAGS}|g" Makefile
  sed -i "s|-O2|${CFLAGS}|g" Makefile-libbz2_so
  
  make -f Makefile-libbz2_so
  make libbz2.a

  install -Dm755 libbz2.so.1.0.6 $pkgdir/usr/lib32/libbz2.so.1.0.6
  ln -s libbz2.so.1.0.6 $pkgdir/usr/lib32/libbz2.so
  ln -s libbz2.so.1.0.6 $pkgdir/usr/lib32/libbz2.so.1
  ln -s libbz2.so.1.0.6 $pkgdir/usr/lib32/libbz2.so.1.0
  
  install -Dm644 libbz2.a ${pkgdir}/usr/lib32/libbz2.a
}
