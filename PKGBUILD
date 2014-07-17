# $Id: PKGBUILD 113090 2014-06-13 12:23:45Z lcarlier $
# Maintainer: Biru Ionut <ionut@archlinux.ro>
# Contributor: Mikko Seppälä <t-r-a-y@mbnet.fi>
# Contributor: Kaos < gianlucaatlas dot gmail dot com >

_pkgbasename=sqlite
pkgname=lib32-sqlite
_amalgamationver=3080500
_docver=${_amalgamationver}
#_docver=3080401
pkgver=3.8.5
pkgrel=1
pkgdesc="A C library that implements an SQL database engine (32-bit)"
arch=('x86_64')
license=('custom')
url="http://www.sqlite.org/"
depends=(lib32-glibc $_pkgbasename)
makedepends=('tcl' 'gcc-multilib' 'lib32-readline')
source=(http://www.sqlite.org/2014/sqlite-autoconf-${_amalgamationver}.tar.gz)
sha1sums=('7f667e10ccebc26ab2086b8a30cb0a600ca0acae')
provides=("lib32-sqlite3=$pkgver")
replaces=("lib32-sqlite3")
conflicts=("lib32-sqlite3")

build() {
  cd ${srcdir}/sqlite-autoconf-${_amalgamationver}

  export CC="gcc -m32"
  export CXX="g++ -m32"
  export PKG_CONFIG_PATH="/usr/lib32/pkgconfig"

  export LTLINK_EXTRAS="-ldl"
  export CFLAGS="$CFLAGS -DSQLITE_ENABLE_FTS3=1 -DSQLITE_ENABLE_COLUMN_METADATA=1 -DSQLITE_ENABLE_UNLOCK_NOTIFY -DSQLITE_SECURE_DELETE"

  ./configure --prefix=/usr --libdir=/usr/lib32 \
    --disable-static

  make
}


package() {
  cd ${srcdir}/sqlite-autoconf-${_amalgamationver}

  make DESTDIR=${pkgdir} install

  rm -rf "${pkgdir}"/usr/{include,share,bin}
  mkdir -p "$pkgdir/usr/share/licenses"
  ln -s $_pkgbasename "$pkgdir/usr/share/licenses/$pkgname"
}
