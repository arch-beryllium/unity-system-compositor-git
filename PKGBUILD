pkgname=unity-system-compositor-git
_pkgname=unity-system-compositor
pkgver=r1173.75d2724
pkgrel=1
pkgdesc='Unity Compositor for Mir'
url='https://github.com/ubports/unity-system-compositor/tree/xenial_-_edge_-_wayland'
arch=(x86_64 i686 armv7h aarch64)
license=()
conflicts=(unity-system-compositor)
provides=(unity-system-compositor)
depends=(boost mir dbus gdk-pixbuf2 glib2 mesa glm wayland deviceinfo)
makedepends=(git gmock cmake cmake-extras)
source=('git+https://github.com/ubports/unity-system-compositor.git#branch=xenial_-_edge_-_wayland'
        'logo.png'
        'blue-dot.png')
sha256sums=('SKIP'
            '376b1daf075635d80bb9137e966dcc67169e5241463bfcecc2d7b7cec92f3538'
            '2d8b7209d2727e79005a89114ff874de83572497ffa339548859118b13dd7bc7')

pkgver() {
 cd ${_pkgname}
 printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare() {
  cd ${_pkgname}
  cp ../logo.png spinner/logo.png
  cp ../logo.png spinner/robot.png
  cp ../blue-dot.png spinner/orange-dot.png
}

build() {
  cd ${_pkgname}
  mkdir -p build
  cd build
  cmake ../ -DCMAKE_INSTALL_PREFIX:PATH=/usr -DCMAKE_INSTALL_LIBDIR="lib/" -DCMAKE_INSTALL_SYSCONFDIR=/etc -DCMAKE_INSTALL_LOCALSTATEDIR=/var
  make
}

package() {
  cd ${_pkgname}/build
  make DESTDIR="${pkgdir}/" install
  mv "${pkgdir}/usr/sbin/unity-system-compositor"  "${pkgdir}/usr/bin"
  rm -r "${pkgdir}/usr/sbin/"
}
