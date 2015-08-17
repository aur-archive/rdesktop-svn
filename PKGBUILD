# Contributor: Frank Oosterhuis <frank@scriptzone.nl>
# Contributor: Aaron Lindsay <aaron@aaronlindsay.com>
# Contributor: James (setkeh) Griffis <setkeh@gmail.com>

pkgname=rdesktop-svn
pkgver=1836
pkgrel=1
arch=('x86_64' 'i686')
pkgdesc="rdesktop is an open source client for Windows Terminal Services"
url="http://www.rdesktop.org"
license=('GPL')
depends=('libx11' 'openssl' 'libao' 'libsamplerate' 'pcsclite')
makedepends=('subversion')
provides=('rdesktop=1.8.2')
conflicts=('rdesktop')

package() {
_svntrunk=http://svn.code.sf.net/p/rdesktop/code/rdesktop/trunk/
_svnmod=rdesktop

  cd "$srcdir"

  if [ -d $_svnmod/.svn ]; then
    (cd $_svnmod && svn up -r $pkgver)
  else
    svn co $_svntrunk --config-dir ./ -r $pkgver $_svnmod
  fi

  msg "SVN checkout done or server timeout"
  msg "Starting make..."

  rm -rf "$srcdir/$_svnmod-build"
  cp -r "$srcdir/$_svnmod" "$srcdir/$_svnmod-build"
  cd "$srcdir/$_svnmod-build"

  ./bootstrap
  ./configure --prefix=/usr
  make || return 1
  make DESTDIR="$pkgdir/" install
}
