
# Maintainer: eXhumer <eXhumer@member.fsf.org>
pkgname=switch-ex-curl
pkgver=7.69.1
pkgrel=2
pkgdesc='An URL retrieval utility and library'
arch=('any')
url='http://www.zlib.net/'
license=('zlib')
options=(!strip libtool staticlibs)
depends=('switch-zlib' 'libnx' 'switch-mbedtls')
conflicts=('switch-curl')
provides=('switch-curl')
replaces=('switch-curl')
makedepends=('switch-pkg-config' 'devkitpro-pkgbuild-helpers')
source=(
    "https://curl.haxx.se/download/curl-${pkgver}.tar.xz"
    'switch-curl.patch'
)
groups=('switch-portlibs')

sha256sums=(
 '03c7d5e6697f7b7e40ada1b2256e565a555657398e6c1fcfa4cb251ccd819d4f'
 'b5e69be885819c82666a70ef40bc53e8072e4210ca2c24f6ddc5d4b289e8cc82'
)

build() {
  cd curl-$pkgver

  patch -Np1 -i $srcdir/switch-curl.patch

  source /opt/devkitpro/switchvars.sh

  ./buildconf

  ./configure --prefix=$PORTLIBS_PREFIX --host=aarch64-none-elf \
    --disable-shared --enable-static --disable-ipv6 --disable-unix-sockets \
    --disable-manual --disable-ntlm-wb --disable-threaded-resolver \
    --without-ssl --without-polar-ssl --without-cyassl --without-wolfssl \
    --with-mbedtls --with-libnx --with-default-ssl-backend=mbedtls

  make -C lib
  
}

package() {
  cd curl-$pkgver

  source /opt/devkitpro/switchvars.sh

  make DESTDIR="$pkgdir" -C lib install
  make DESTDIR="$pkgdir" -C include install
  make DESTDIR="$pkgdir" install-binSCRIPTS

}