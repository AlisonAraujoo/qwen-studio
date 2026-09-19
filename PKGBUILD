# Maintainer: Alison Araújo
pkgname=qwen-studio
pkgver=2.2.3
pkgrel=2
pkgdesc="Open-source Qwen AI desktop client for Linux with MCP support (Tauri v2)"
arch=('x86_64')
url="https://github.com/AlisonAraujoo/qwen-studio"
license=('MIT')
depends=(
    'webkit2gtk-4.1'
    'gtk3'
    'libappindicator-gtk3'
    'libayatana-appindicator'
    'openssl'
    'librsvg'
    'gst-plugins-base'
)
makedepends=(
    'git'
    'nodejs>=18'
    'npm'
    'rustup'
)
provides=('qwen-studio')
conflicts=('qwen-studio-bin')
source=("git+https://github.com/AlisonAraujoo/qwen-studio.git")
sha256sums=('SKIP')

prepare() {
    cd "$srcdir/$pkgname"
    rustup toolchain install stable --profile minimal
    rustup default stable
    npm install --prefer-offline
}

build() {
    cd "$srcdir/$pkgname"
    npm run tauri:build -- --bundles none
}

package() {
    cd "$srcdir/$pkgname"
    install -Dm755 "target/release/$pkgname" "$pkgdir/usr/bin/$pkgname"
    install -Dm644 "icon.png" "$pkgdir/usr/share/icons/hicolor/512x512/apps/$pkgname.png"
    install -Dm644 "$pkgname.desktop" "$pkgdir/usr/share/applications/$pkgname.desktop"
    install -Dm644 "README.md" "$pkgdir/usr/share/doc/$pkgname/README.md"
    if [[ -f "LICENSE" ]]; then
        install -Dm644 "LICENSE" "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
    fi
}
