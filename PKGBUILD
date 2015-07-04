pkgname=supertuxkart
pkgver=0.9
pkgrel=1
pkgdesc='Kart racing game featuring Tux and his friends'
arch=('x86_64')
url='http://supertuxkart.sourceforge.net/'
license=('GPL2')
depends=('openal' 'libvorbis' 'fribidi' 'curl' 'bluez' 'libxrandr' 'glu')
makedepends=('cmake' 'subversion' 'mesa' 'imagemagick' 'setconf' 'mesa')
source=("http://downloads.sourceforge.net/$pkgname/$pkgname-$pkgver-src.tar.xz")
install=supertuxkart.install
md5sums=('ae07569ab02c88ca4d49017df7731923')

build() {
  cd ${srcdir}/supertuxkart-${pkgver}

  _fn="data/${pkgname}.desktop"
  setconf "$_fn" Exec "$pkgname"
  setconf "$_fn" TryExec "$pkgname"
  setconf "$_fn" Icon "$pkgname"_128

  [[ -d build ]] && rm -r build
  mkdir build && cd build

  cmake .. \
    -DIRRLICHT_DIR="$srcdir/irrlicht" \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DCMAKE_CXX_FLAGS="-lpthread -lm -ldl $CXXFLAGS"

  make
}

package() {
  cd ${srcdir}/supertuxkart-${pkgver}

  cd build
  make DESTDIR=${pkgdir} install
}

# vim:set ts=2 sw=2 et:
