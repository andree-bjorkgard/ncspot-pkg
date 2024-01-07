pkgname=ncspot
pkgver=1.0.0
pkgrel=4
pkgdesc="Cross-platform ncurses Spotify client written in Rust, inspired by ncmpc and the likes."
arch=('x86_64')
url="https://github.com/hrkfdn/ncspot"
license=('BSD')
depends=('openssl' 'libpulse' 'libxcb' 'dbus' 'hicolor-icon-theme')
makedepends=('cargo' 'python' 'pkgconf' 'ueberzug')
optdepends=('ueberzug: display album art in terminal (X11)')
source=("${pkgname}-${pkgver}.tar.gz::https://github.com/hrkfdn/ncspot/archive/v${pkgver}.tar.gz")
sha256sums=('516663b62b9536cb18e6d8eb69470a5b6560f2890e010e8a3d2e8cfc65df9497')
options=('!lto')

prepare() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  export RUSTUP_TOOLCHAIN=stable
  export CARGO_TARGET_DIR=target
  cargo build --frozen --release --features cover
}

check() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  export RUSTUP_TOOLCHAIN=stable
  cargo test --frozen --features cover
}

package() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  install -Dm 755 "target/release/${pkgname}" "${pkgdir}/usr/bin/${pkgname}"
  install -Dm 644 "misc/ncspot.desktop" "${pkgdir}/usr/share/applications/ncspot.desktop"
  install -Dm 644 "images/logo.svg" "${pkgdir}/usr/share/icons/hicolor/scalable/apps/ncspot.svg"
  install -Dm 644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
