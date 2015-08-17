# Maintainer: Raziel23 <venom23 at runbox dot com>
# Contributor: Kevin Whitaker <eyecreate at gmail dot com>

pkgname=vcmi-svn
pkgver=3798
pkgrel=1
pkgdesc="Heroes of Might and Magic 3 game engine"
arch=('i686' 'x86_64')
url="http://forum.vcmi.eu/portal.php"
license=('GPL')
depends=('boost-libs' 'ffmpeg' 'sdl_image' 'sdl_mixer' 'sdl_ttf' 'qt5-base' 'desktop-file-utils' 'gtk-update-icon-cache' 'hicolor-icon-theme')
makedepends=('boost' 'cmake' 'subversion')
optdepends=('innoextract: required by vcmibuilder'
            'unshield: required by vcmibuilder'
            'unzip: required by vcmibuilder'
            'wget: required by vcmibuilder')
provides=('vcmi')
conflicts=('vcmi')
install=vcmi-svn.install
_svnmod=vcmi
source=("$_svnmod::svn+https://svn.code.sf.net/p/vcmi/code/trunk/")
md5sums=('SKIP')

pkgver() {
  svnversion "$srcdir/$_svnmod" | tr -d [A-z]
}

prepare() {
  cd "$srcdir"

  if [[ -d "$_svnmod-build" ]]; then
    msg 'Removing the last build...'
    rm -rf "$_svnmod-build"
  fi

  mkdir "$_svnmod-build"
}

build() {
  cd "$srcdir/$_svnmod-build"

  cmake "../$_svnmod" \
    -DCMAKE_INSTALL_PREFIX='/usr' \
    -DCMAKE_INSTALL_LIBDIR='lib' \
    -DCMAKE_SKIP_RPATH='OFF' \
    -DCMAKE_BUILD_TYPE='Debug'
  make
}

package() {
  cd "$srcdir/$_svnmod-build"
  make DESTDIR="$pkgdir" install
}

# vim:set ts=2 sw=2 et:
