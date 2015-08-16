# Maintainer: Naelstrof <naelstrof@gmail.com> 
pkgname=mingw-w64-enet
pkgver=1.3.12
pkgrel=3
pkgdesc="A free, open source, portable framework for networking application development (mingw-w64)"
arch=('any')
url="http://enet.bespin.org/"
license=('MIT')
makedepends=('mingw-w64-gcc')
depends=('mingw-w64-crt')
options=('!strip' '!buildflags' 'staticlibs')
source=("http://enet.bespin.org/download/enet-${pkgver}.tar.gz")
md5sums=('2b581600a589553c1e7684ad663f27a8')

_architectures="i686-w64-mingw32 x86_64-w64-mingw32"

build() {
    #required else the compile fails.
    cp -rf ${srcdir}/enet-${pkgver}/include/enet ${srcdir}/enet-${pkgver}
    unset LDFLAGS
    for _arch in ${_architectures}; do
        mkdir -p ${srcdir}/enet-${pkgver}-build-${_arch}
        cd ${srcdir}/enet-${pkgver}-build-${_arch}
        ${srcdir}/enet-${pkgver}/configure --prefix=/usr/${_arch} --build=$CHOST --host=${_arch}
        make
    done
}

package() {
    for _arch in ${_architectures}; do
        cd ${srcdir}/enet-${pkgver}-build-${_arch}
        make DESTDIR=${pkgdir} install
        mkdir -p "${pkgdir}/usr/${_arch}/share/licenses/${pkgname}"
        cp "${srcdir}/enet-${pkgver}/LICENSE" "${pkgdir}/usr/${_arch}/share/licenses/${pkgname}"
        # no need to strip??
        #${_arch}-strip --strip-unneeded "$pkgdir"/usr/${_arch}/bin/*.dll
        #${_arch}-strip -g "$pkgdir"/usr/${_arch}/lib/*.a
    done
}
