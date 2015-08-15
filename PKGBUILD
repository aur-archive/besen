pkgname=besen
pkgver=12
pkgrel=5
pkgdesc="Complete ECMAScript Fifth Edition Implemention in Object Pascal"
arch=(i686 x86_64)
license=("LGPL")
depends=("fpc>=2.6.0")
makedepends=(subversion)
url="http://code.google.com/p/besen"
_svntrunk="http://besen.googlecode.com/svn/trunk/"
_svnmod="besen"
_unittgt=`fpc -iSP`-`fpc -iSO`
_fpcver=`fpc -iV`

build() {
  cd "${srcdir}"

  if [ -d "${_svnmod}/.svn" ]; then
    (cd "$_svnmod" && svn up -r $pkgver)
  else
    svn co "$_svntrunk" --config-dir ./ -r $pkgver $_svnmod
  fi

  msg 'SVN checkout done or server timeout'

  rm -rf "${_svnmod}-build"
  cp -r "$_svnmod" "${_svnmod}-build"
  cd "${_svnmod}-build/src"
  
  fpc BESEN.pas
  fpc BESEN.pas
  fpc BESEN.pas
  fpc BESEN.pas
  fpc BESEN.pas
}

package() {
  cd "${_svnmod}-build"
  install -Dm644 copying.besen "$pkgdir/usr/share/licenses/$pkgname/copying.besen"
  install -m644 copying.txt "$pkgdir/usr/share/licenses/$pkgname/"
  cd "src"
  find . -name '*.o' -o -name '*.ppu' -o -name '*.rst' -o -name '*.a' |
    xargs -rtl1 -I {} install -Dm644 {} "$pkgdir/usr/lib/fpc/$_fpcver/units/$_unittgt/besen/"{}
}
