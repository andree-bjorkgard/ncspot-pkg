pkgname=ncspot
pkgver=1.2.0
pkgrel=5
pkgdesc="Cross-platform ncurses Spotify client written in Rust, inspired by ncmpc and the likes."
arch=('x86_64')
url="https://github.com/hrkfdn/ncspot"
license=('BSD')
depends=('openssl' 'libpulse' 'libxcb' 'dbus' 'hicolor-icon-theme')
makedepends=('cargo' 'python' 'pkgconf' 'ueberzug')
optdepends=('ueberzug: display album art in terminal (X11)')
source=("${pkgname}-${pkgver}.tar.gz::https://github.com/hrkfdn/ncspot/archive/v${pkgver}.tar.gz")
sha256sums=('0df821a5ea70a143d3529abadd39bcdd9643720a602c99a9c0f8f31f52b4a0fb')
options=('!lto')

prepare() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  export RUSTUP_TOOLCHAIN=stable
  export CARGO_TARGET_DIR=target
  cargo build --frozen
}

check() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  export RUSTUP_TOOLCHAIN=stable
  cargo test --frozen
}

package() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  install -Dm 755 "target/release/${pkgname}" "${pkgdir}/usr/bin/${pkgname}"
  install -Dm 644 "misc/ncspot.desktop" "${pkgdir}/usr/share/applications/ncspot.desktop"
  install -Dm 644 "images/logo.svg" "${pkgdir}/usr/share/icons/hicolor/scalable/apps/ncspot.svg"
  install -Dm 644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
