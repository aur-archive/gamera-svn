# Maintainer: Quentin Stievenart <acieroid@awesom.eu>
# Contributor: Abakus <java5@arcor.de>

pkgname=gamera-svn
pkgver=1219
pkgrel=1
pkgdesc="a framework for building document analysis applications"
arch=('i686' 'amd64')
url="http://gamera.informatik.hsnr.de/"
license=('GPL')
depends=('python2' 'wxpython' 'libtiff' 'libpng')
makedepends=('svn' 'gcc')
provides=('gamera')
conflicts=('gamera')

_svntrunk="https://gamera.svn.sourceforge.net/svnroot/gamera/trunk/gamera"
_svnmod=gamera

build() {
  cd $startdir/src
  msg "Connecting to SVN server...."
  if [ -d $_svnmod/.svn ]; then
    (cd $_svnmod && svn up -r $pkgver)
  else
    svn co $_svntrunk --config-dir ./ -r $pkgver $_svnmod
  fi

  msg "SVN checkout done or server timeout"
  msg "Starting make..."
  cd $_svnmod
  python2 setup.py build
  python2 setup.py install --root=$pkgdir/ --optimize=1 || return 1

  # Remember to install licenses if the license is not a common license!
  # install -D -m644 $srcdir/LICENSE $pkgdir/usr/share/licenses/$pkgname/LICENSE
}

