# Maintainer: Andrea Scarpino <andrea@archlinux.org>

pkgname=kwallet-git
pkgver=6.3.0.r1456.425cf15f
pkgrel=1
pkgdesc='KWallet Framework'
arch=(x86_64)
url='https://projects.kde.org/projects/frameworks/kwallet'
license=(LGPL)
depends=(knotifications-git kiconthemes-git kservice-git gpgme qca-qt6)
makedepends=(extra-cmake-modules-git git python boost kdoctools-git)
conflicts=(kwallet kwallet5)
provides=(kwallet kwallet5)
source=('git+https://github.com/KDE/kwallet.git')
md5sums=('SKIP')

pkgver() {
  cd kwallet
  _ver="$(cat CMakeLists.txt | grep -m1 'KF_VERSION' | grep -o "[[:digit:]]*" | paste -sd'.')"
  echo "${_ver}.r$(git rev-list --count HEAD).$(git rev-parse --short HEAD)"
}

prepare() {
  mkdir -p build
}

build() {
  cd build
  cmake ../kwallet \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DKDE_INSTALL_LIBDIR=lib \
    -DKDE_INSTALL_USE_QT_SYS_PATHS=ON \
    -DBUILD_TESTING=OFF \
    -DQT_MAJOR_VERSION=6
  make
}

package() {
  cd build
  make DESTDIR="$pkgdir" install
}
