pkgname=rpicam-apps
pkgver=1.8.1
pkgrel=1
pkgdesc="Raspberry Pi libcamera-based camera applications (rpicam-*)"
arch=('aarch64' 'armv7h')
url="https://github.com/raspberrypi/rpicam-apps"
license=('BSD')
depends=(
  'libcamera'
  'libjpeg-turbo'
  'libtiff'
  'libpng'
  'libdrm'
  'libexif'
  'boost-libs'
  'opencv'
)
makedepends=(
  'cmake'
  'git'
  'boost'
  'meson'
)
source=("${pkgname}-${pkgver}.tar.gz::https://github.com/raspberrypi/rpicam-apps/archive/refs/tags/v${pkgver}.tar.gz")
sha256sums=('a7c8c5e3925d62411e5a8f4d0a4c731088bea420266cf8ec2e0386069b811e92')

build() {
  meson setup build ${pkgname}-${pkgver} -Denable_libav=disabled -Denable_drm=enabled -Denable_egl=disabled -Denable_qt=disabled -Denable_opencv=enabled -Denable_tflite=disabled -Denable_hailo=disabled --prefix=/usr
  meson compile -C build
}

package() {
  meson install -C build --destdir "$pkgdir"

  if [[ -f "${srcdir}/${pkgname}-${pkgver}/license.txt" ]]; then
    install -Dm644 "${srcdir}/${pkgname}-${pkgver}/license.txt" "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
  fi
}
