# Maintainer: Edward Davis <idlyby@proton.me>
# Contributor: alba4k <blaskoazzolaaaron@gmail.com>

_pkgname="hyprlock"
pkgname="${_pkgname}-git"
pkgver=0.5.0.r4.gedbecc87
pkgrel=1
pkgdesc=" Hyprland's GPU-accelerated screen locking utility "
arch=(any)
url="https://github.com/hyprwm/hyprlock"
license=('BSD-3-Clause')
depends=('wayland' 'hyprlang-git' 'cairo' 'pango' 'pam' 'libxkbcommon' 'libglvnd' 'libdrm' 'mesa' 'libjpeg' 'libwebp' 'hyprutils-git' 'file' 'sdbus-cpp-git')
makedepends=('git' 'cmake' 'gcc' 'wayland-protocols' 'xorgproto')
source=("${_pkgname}::git+https://github.com/hyprwm/hyprlock.git")
conflicts=("${_pkgname}")
provides=("${_pkgname}")
sha256sums=('SKIP')

backup=('etc/pam.d/hyprlock')

pkgver() {
    cd ${_pkgname}

    git describe --long --tags --abbrev=8 --exclude='*[a-zA-Z][a-zA-Z]*' \
      | sed -E 's/^[^0-9]*//;s/([^-]*-g)/r\1/;s/-/./g'
}

build() {
	cd "${srcdir}/${_pkgname}"

	cmake --no-warn-unused-cli -DCMAKE_BUILD_TYPE:STRING=Release -DCMAKE_INSTALL_PREFIX=/usr -S . -B ./build
    cmake --build ./build --config Release --target hyprlock
}

package() {
	cd "${srcdir}/${_pkgname}"

	DESTDIR="${pkgdir}" cmake --install build

	install -Dm644 LICENSE -t "${pkgdir}/usr/share/licenses/${pkgname}"
}

