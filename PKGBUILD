# Maintainer: James Ward <james@notjam.es>

pkgname=spriter
pkgver=R7
pkgrel=1
pkgdesc="2D Game Sprite Animation and Object Creation Tool"
arch=('i686' 'x86_64')
url="http://brashmonkey.com/spriter.htm"
license=('custom')
depends=('qt5-script' 'qt5-multimedia' 'qt5-webkit' 'qt5-tools' 'libpng12' 'imagemagick>=7.0.0')
makedepends=('chrpath')

if [[ "$CARCH" == "x86_64" ]]; then
  _arch=64
  source=("http://www.brashmonkeygames.com/spriter/legacyVersions/r7-3-18-2016/SpriterR7(64).tar.gz")
  sha256sums=('f00a2d634ec952dd5cdead67e65ec286dd2070d84141b45f2d97d232743fdb97')
elif [[ "$CARCH" == "i686" ]]; then
  _arch=32
  source=("http://www.brashmonkeygames.com/spriter/legacyVersions/r7-3-18-2016/SpriterR7(32).tar.gz")
  sha256sums=('5138b6e26b29ab53e72382dedaf37e0b7e9b0a10b2eca31b5710e59e30729f09')
fi

package() {
  cd "$srcdir/Spriter${pkgver^^}($_arch)"

  install -d "$pkgdir/usr/bin/"

  install -dm755 "$pkgdir/opt/spriter/"
  install -dm755 "$pkgdir/opt/spriter/TexturePackerTemplates/"
  install -dm755 "$pkgdir/opt/spriter/plugins/"
  install -dm755 "$pkgdir/opt/spriter/lib/"

  install -Dm644 SpriterEULA.txt "$pkgdir/usr/share/licenses/$pkgname/SpriterEULA.txt"

  install -m644 SpriterHelp.* "$pkgdir/opt/spriter/"

  install -m755 Spriter "$pkgdir/opt/spriter/spriter.bin"
  chrpath -d "$pkgdir/opt/spriter/spriter.bin"

  install -m644 TexturePackerTemplates/* "$pkgdir/opt/spriter/TexturePackerTemplates"

  # Seems we need these too
  install -m644 libsteam_api.so "$pkgdir/opt/spriter/lib"
  install -m644 png.so "$pkgdir/opt/spriter/lib"
  install -m644 png.la "$pkgdir/opt/spriter/lib"


  cp -a docs "$pkgdir/opt/spriter/"
  printf "#!/bin/sh\ncd /opt/spriter/\nexport LD_LIBRARY_PATH=\"/opt/spriter/lib/\"\n./spriter.bin\n" > "$pkgdir/usr/bin/spriter"
  chmod 755 "$pkgdir/usr/bin/spriter"
}
