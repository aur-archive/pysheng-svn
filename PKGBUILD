# This is an example PKGBUILD file. Use this as a start to creating your own,
# and remove these comments. For more information, see 'man PKGBUILD'.
# NOTE: Please fill out the license field for your package! If it is unknown,
# then please put 'unknown'.

# See http://wiki.archlinux.org/index.php/VCS_PKGBUILD_Guidelines
# for more information on packaging from SVN sources.

# Maintainer: Peter Feigl <craven@gmx.net>
pkgname=pysheng-svn
pkgver=33
pkgrel=1
pkgdesc="CLI and GUI program to download pages from Google Books as PNG images"
arch=(i686 x86_64)
url="https://code.google.com/p/pysheng/"
license=('GPL')
depends=('python2')
makedepends=('subversion')
optdepends=('python2-reportlab: GUI'
	    'pygtk: GUI')
provides=()
conflicts=(pysheng)
replaces=()
options=()
noextract=()

_svntrunk=http://pysheng.googlecode.com/svn/trunk/
_svnmod=pysheng

build() {
  cd "$srcdir"
  msg "Connecting to SVN server...."

  if [[ -d "$_svnmod/.svn" ]]; then
    (cd "$_svnmod" && svn up -r "$pkgver")
  else
    svn co "$_svntrunk" --config-dir ./ -r "$pkgver" "$_svnmod"
  fi

  msg "SVN checkout done or server timeout"
  msg "Starting build..."

  rm -rf "$srcdir/$_svnmod-build"
  svn export "$srcdir/$_svnmod" "$srcdir/$_svnmod-build"
  cd "$srcdir/$_svnmod-build"

  #
  # BUILD HERE
  #
   python2 setup.py install --root="$pkgdir/" --optimize=1
}

# vim:set ts=2 sw=2 et:
