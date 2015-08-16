# Maintainer: Spyhawk

# in case of memory issues, consider using MAKEFLAGS="-j1" to compile

pkgname=libzypp-bindings-git
pkgver=0.6.3
pkgrel=1
pkgdesc="Package, Patch, Pattern, and Product Management"
arch=('i686' 'x86_64')
url="https://github.com/openSUSE/libzypp-bindings"
license=('GPL')
depends=('libzypp-git' 'python2' 'perl' 'ruby')
makedepends=('git' 'cmake' 'boost' 'swig2')
provides=('libzypp-bindings')
conflicts=('libzypp-bindings')
source=('git+https://github.com/openSUSE/libzypp-bindings.git'
        'make-ZyppCommon-cmake-module-includable.patch')
md5sums=('SKIP'
         '71d063d865f99ac00ab24cf759107376')
_gitname="libzypp-bindings"

pkgver() {
    cd "$srcdir/$_gitname"
    echo $(git describe --always | sed -r 's/-/./g')
}

prepare() {
    cd "$srcdir/$_gitname"
    patch -p1 -i $srcdir/make-ZyppCommon-cmake-module-includable.patch
}

build() {
    cd "$srcdir/$_gitname"
    cmake -D CMAKE_INSTALL_PREFIX=/usr \
        -D CMAKE_BUILD_TYPE=Release \
        -D LIB=/lib \
        -D ZYPP_PREFIX=/usr \
        -D SWIG_EXECUTABLE=/usr/bin/swig-2 \
        -D PYTHON_EXECUTABLE=/usr/bin/python2 \
        -D RUBY_VENDORARCH_DIR=/tmp \
        -D CMAKE_VERBOSE_MAKEFILE=TRUE \
        .
    make
}

package() {
    cd "$srcdir/$_gitname"
    make DESTDIR="$pkgdir/" install
}
