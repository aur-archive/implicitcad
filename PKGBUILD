# Maintainer: Brad Pitcher <bradpitcher@gmail.com>
_hkgname=implicit
pkgname=implicitcad
pkgver=0.0.3
pkgrel=3
pkgdesc="Math-inspired programmatic 2&3D CAD: CSG, bevels, and shells; gcode export.."
url="http://hackage.haskell.org/package/${_hkgname}"
license=('GPL')
arch=('i686' 'x86_64')
makedepends=()
depends=('ghc' 'haskell-juicypixels' 'haskell-blaze-builder' 'haskell-blaze-markup' 'haskell-blaze-svg' 'haskell-bytestring>=0.9.1.10' 'haskell-containers>=0.4.0.0' 'haskell-deepseq>=1.1.0.2' 'haskell-directory>=1.1.0.0' 'haskell-filepath>=1.2.0.0' 'haskell-mtl>=2.0.1.0' 'haskell-optparse-applicative' 'haskell-parallel>=3.1.0.1' 'haskell-parsec>=3.1.1' 'haskell-storable-endian' 'haskell-text>=0.11.0.5' 'haskell-unordered-containers' 'haskell-vector-space')
options=('strip')
source=(http://hackage.haskell.org/packages/archive/${_hkgname}/${pkgver}/${_hkgname}-${pkgver}.tar.gz)
install=${pkgname}.install
md5sums=('91e94cb31caeb4f07e97f7939cc770f9')
build() {
    cd ${srcdir}/${_hkgname}-${pkgver}
    runhaskell Setup configure -O ${PKGBUILD_HASKELL_ENABLE_PROFILING:+-p } --enable-split-objs --enable-shared \
       --prefix=/usr --docdir=/usr/share/doc/${pkgname} --libsubdir=\$compiler/site-local/\$pkgid
    runhaskell Setup build --ghc-options=-XOverlappingInstances
    runhaskell Setup haddock
    runhaskell Setup register   --gen-script
    runhaskell Setup unregister --gen-script
    sed -i -r -e "s|ghc-pkg.*unregister[^ ]* |&'--force' |" unregister.sh
}
package() {
    cd ${srcdir}/${_hkgname}-${pkgver}
    install -D -m744 register.sh   ${pkgdir}/usr/share/haskell/${pkgname}/register.sh
    install    -m744 unregister.sh ${pkgdir}/usr/share/haskell/${pkgname}/unregister.sh
    install -d -m755 ${pkgdir}/usr/share/doc/ghc/html/libraries
    ln -s /usr/share/doc/${pkgname}/html ${pkgdir}/usr/share/doc/ghc/html/libraries/${_hkgname}
    runhaskell Setup copy --destdir=${pkgdir}
}
