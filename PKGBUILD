# Maintainer: Alison Araújo
pkgname=qwen-studio
pkgver=2.2.3
pkgrel=1
pkgdesc="Open-source Qwen AI desktop client for Linux with MCP support (Tauri v2)"
arch=('x86_64')
url="https://github.com/AlisonAraujoo/qwen-studio"
license=('MIT')
depends=(
    'webkit2gtk-4.1'
    'gtk3'
    'libappindicator-gtk3'
    'openssl'
    'librsvg'
    'libayatana-appindicator'
)
makedepends=(
    'git'
    'nodejs>=18'
    'npm'
    'rustup'
    'cargo'
)
provides=('qwen-studio')
conflicts=('qwen-studio-bin')
source=("git+https://github.com/AlisonAraujoo/qwen-studio.git")
sha256sums=('SKIP')

prepare() {
    cd "$srcdir/$pkgname"
    
    # Garante toolchain Rust estável
    rustup toolchain install stable --profile minimal
    rustup default stable
    
    # Instala dependências Node.js
    npm install --prefer-offline
}

build() {
    cd "$srcdir/$pkgname"
    
    # Build de produção otimizado
    npm run tauri:build
}

package() {
    cd "$srcdir/$pkgname"
    
    # Binário compilado
    install -Dm755 "src-tauri/target/release/$pkgname" \
        "$pkgdir/usr/bin/$pkgname"
    
    # Ícones em múltiplos tamanhos
    install -Dm644 "icon.png" \
        "$pkgdir/usr/share/icons/hicolor/512x512/apps/$pkgname.png"
    
    # Desktop entry
    install -Dm644 "$pkgname.desktop" \
        "$pkgdir/usr/share/applications/$pkgname.desktop"
    
    # Documentação
    install -Dm644 "README.md" \
        "$pkgdir/usr/share/doc/$pkgname/README.md"
    
    # Licença (extrai do README se não houver LICENSE)
    if [[ -f "LICENSE" ]]; then
        install -Dm644 "LICENSE" "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
    fi
}
