# Maintainer: Cravix < dr dot neemous at gmail dot org >
# Based on edje PKGBUILD wrote by Ronald van Haren <ronald.archlinux.org>


pkgname=terminology-svn
pkgver=79869
pkgrel=3
pkgdesc="Terminal emulator for e17, successor of previous eterm"
arch=('i686' 'x86_64')
groups=('e17-extra-svn')
url="http://www.enlightenment.org/p.php?p=about/terminology"
license=('BSD')
depends=('efl-git' 'elementary-git')
makedepends=('svn')
provides=('terminology')
conflicts=('terminology')
options=('!libtool')

_svntrunk="http://svn.enlightenment.org/svn/e/trunk/terminology"
_svnmod="terminology"

build() {
  
  echo -e "\033[31;1;5m If error occurs when building, you may need to upgrade e17 libs from svn to keep consistency with current API ."
  echo -e "\033[31;1;5m You can use my script at\033[36;5m http://code.google.com/p/projectf/downloads/list \033[31;1;5m to do that."
  sleep 2

  cd $srcdir

  msg "Connecting to $_svntrunk SVN server...."
  if [ -d $_svnmod/.svn ]; then
    (cd $_svnmod && svn up -r $pkgver)
  else
    svn co $_svntrunk --config-dir ./ -r $pkgver $_svnmod
  fi

  msg "SVN checkout done or server timeout"
  msg "Starting make..."

  cp -r $_svnmod $_svnmod-build
  cd $_svnmod-build

  ./autogen.sh --prefix=/usr
  make
}

package(){
  cd $srcdir/$_svnmod-build
  make DESTDIR=$pkgdir install

# install license files
  install -Dm644 $srcdir/$_svnmod-build/COPYING \
        $pkgdir/usr/share/licenses/$pkgname/COPYING

  rm -r $srcdir/$_svnmod-build

}
