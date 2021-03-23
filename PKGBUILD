# Maintainer: Térence Clastres <t dot clastres at gmail dot com>
# PKGBUILD based on the one from https://aur.archlinux.org/packages/lite

pkgname=lite-xl
_pkgname=lite
pkgver=1.16.5
pkgrel=2
pkgdesc='A lightweight text editor written in Lua'
arch=('x86_64')
url="https://github.com/franko/$pkgname"
license=('MIT')
depends=('agg' 'lua52' 'sdl2')
makedepends=('meson' 'gendesk')
conflicts=("$_pkgname")
provides=("$_pkgname")
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('2f02e0460bd628f068461c5098a4c651cbfc6471b0c41f0b6252aa9e4a9dbe8d')

prepare() {
    cd "$pkgname-$pkgver"

  # XDG desktop file
  gendesk -n -f \
          --pkgname "$pkgname" \
          --pkgdesc "$pkgdesc" \
          --exec "$_pkgname %F" \
          --name "Lite XL" \
          --categories "Utility;TextEditor;Development" \
          --mimetype "text/plain"

}

build() {
    cd "$pkgname-$pkgver"
    arch-meson build
    meson compile -C build
}

package() {
  cd "$pkgname-$pkgver"

  DESTDIR="$pkgdir" meson install -C build
  
  install -Dm 644 "dev-utils/$_pkgname.svg" \
	"$pkgdir/usr/share/icons/hicolor/scalable/apps/$pkgname.svg"
  install -Dm 644 "$pkgname.desktop" -t "$pkgdir/usr/share/applications"
  install -Dm 644 "LICENSE" -t "$pkgdir/usr/share/licenses/$pkgname"
}

