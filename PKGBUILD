# Maintainer: Martell Malone <martell malone at g mail dot com>
# Contributor: Alexey Pavlov <alexpux@gmail.com>
# Contributor: David Macek <david.macek.0@gmail.com>
# Contributor: Renato Silva <br.renatosilva@gmail.com>
# Modification: Hamayama <fkyo0985@gmail.com>

PKGEXT='.pkg.tar.xz'
_realname=winpty-fixes
pkgname="${_realname}"
pkgver=0.4.3
pkgrel=2
pkgdesc="A Windows software package providing an interface similar to a Unix pty-master for communicating with Windows console programs (with some fixes)"
arch=('i686' 'x86_64')
url="https://github.com/Hamayama/winpty-fixes"
license=('MIT')

# Explicitly reference the git version of the indirect dependency mingw-w64-cross-crt
# for avoiding problems with its default provider mingw-w64-cross-crt-clang-git
makedepends=(git tar automake xz
             mingw-w64-cross-gcc
             mingw-w64-cross-crt-git)

#depends=( "ncurses-devel" )
replaces=("winpty-git")
options=('staticlibs' 'strip')
conflicts=(winpty)

# TODO: Replace path_conv with arg_heuristic from MSYS2 runtime
#       See https://github.com/rprichard/winpty/issues/56
source=("${_realname}-${pkgver}.tar.gz::https://github.com/Hamayama/winpty-fixes/archive/main.tar.gz"
        path_conv.cc::'https://github.com/Alexpux/path_convert/raw/master/src/path_conv.cpp'
        path_conv.h::'https://github.com/Alexpux/path_convert/raw/master/src/path_conv.h'
        0001-Apply-POSIX-to-Win-conversion-on-all-arguments-on-MSYS.patch
        0002-fix-path-conversion.patch)

sha256sums=('SKIP'
            '0f1fad5c8dd102690d46b3a785961f0fe9b7c61e5353126915cdf4a1cd0d14ea'
            'c84e4edc5a1e387dc1ea06445db76a7bfe43e816f0c32558ce8d8562378d5782'
            'c9705d86feba11f1155e4259d28131afb14db3c30c17efe96bdd655afa72ee04'
            '47568cc4ee701c936f49bce4958c05b19260bb85a9cdea0ab8b4d9bf8a1133bd')

consolidate() {
  cp ../path_conv.cc src/unix-adapter/path_conv.cc
  cp ../path_conv.h  src/unix-adapter/path_conv.h
}

prepare() {
  #cd "${srcdir}/${_realname}-${pkgver}"
  cd "${srcdir}/${_realname}-main"
  consolidate
  patch -p1 -i ${srcdir}/0001-Apply-POSIX-to-Win-conversion-on-all-arguments-on-MSYS.patch
  patch -p1 -i ${srcdir}/0002-fix-path-conversion.patch
}

build() {
  #cd "${srcdir}/${_realname}-${pkgver}"
  cd "${srcdir}/${_realname}-main"
  ./configure --build=${CHOST} \
    --prefix=/usr

  make UNIX_ADAPTER_EXE=winpty.exe
}

package() {
  #cd "${srcdir}/${_realname}-${pkgver}"
  cd "${srcdir}/${_realname}-main"
  make PREFIX=${pkgdir}/usr UNIX_ADAPTER_EXE=winpty.exe install
}
