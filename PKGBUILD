# Maintainer: Colin Woodbury <colingw@gmail.com>
_hkgname=aura
pkgname=aura
pkgver=1.1.0.0
pkgrel=1
pkgdesc="A package manager for Arch Linux and the AUR written in Haskell."
url="https://github.com/fosskers/aura"
license=('GPL-3')
arch=('i686' 'x86_64')
depends=('gmp' 'pacman' 'ghc' 'haskell-regex-base' 'haskell-regex-pcre' 
         'haskell-curl' 'haskell-json' 'haskell-url' 'haskell-mtl'
         'haskell-parsec')
optdepends=('pacman-color: For coloured pacman output in Aura.')
options=('strip')
source=(https://bitbucket.org/fosskers/aura/downloads/${_hkgname}-${pkgver}.tar.gz)
md5sums=('453645a80866deb4f5a022a306489f86')
build() {
    cd ${srcdir}/${_hkgname}-${pkgver}
    runhaskell Setup configure --prefix=/usr --docdir=/usr/share/doc/${pkgname} -O
    runhaskell Setup build

    # Installing man page
    mkdir -p "$pkgdir/usr/share/man/man8/"
    install -m 644 aura.8 "$pkgdir/usr/share/man/man8/aura.8"

    # Installing bash completions
    mkdir -p "$pkgdir/usr/share/bash-completion/completions/"
    install -m 644 bashcompletion.sh "$pkgdir/usr/share/bash-completion/completions/aura"

    # Installing zsh completions
    mkdir -p "$pkgdir/usr/share/zsh/site-functions/"
    install -m 644 _aura "$pkgdir/usr/share/zsh/site-functions/_aura"

    # Directory for storing PKGBUILDs
    mkdir -p "$pkgdir/var/cache/aura/pkgbuilds"

    # Directory for storing installed package states
    mkdir -p "$pkgdir/var/cache/aura/states"
}
package() {
    cd ${srcdir}/${_hkgname}-${pkgver}
    runhaskell Setup copy --destdir=${pkgdir}
}
