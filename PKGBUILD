# Maintainer: (jmcb) <joelsgp@protonmail.com>
# Contributor: (Joe084) <develon69 at gmail dot com>

pkgname='pico-8'
pkgver='0.2.6b'
pkgrel=2
pkgdesc="A fantasy console for making, sharing and playing tiny games and other computer programs."
arch=('x86_64' 'i686' 'armv7h' 'aarch64')
url="http://www.lexaloffle.com/pico-8.php"
license=('custom:commercial')
depends=('glibc' 'sdl2' 'curl')
optdepends=()
provides=('pico8')

source=("${pkgname}.desktop"
        "${pkgname}.xml")
source_i686=("file://${pkgname}_${pkgver}_i386.zip")
source_x86_64=("file://${pkgname}_${pkgver}_amd64.zip")
source_armv7h=("file://${pkgname}_${pkgver}_raspi.zip")
source_aarch64=("file://${pkgname}_${pkgver}_raspi.zip")

sha256sums=('272f33c38a74456a4d2597a6b1d0c6ee9695d0e47f31ce08018c24a78e62759e'
            'a7cb3f7f991c0ce5fdadf0a5e5f7f0430ad96ea69f3da26357a0c75e2b54217c')
sha256sums_x86_64=('7ca8e9019f73771064859f71302bbc65c6e4042030605f4ee2f2c8c4e29b15d5')
sha256sums_i686=('91942a7226313378f7adde0eccbf0719d28f358db6bdcbdf572d9867f5d68f2e')
sha256sums_armv7h=('54a3c502215ce0f2a07ae35624fed38fbd977a613f0d1366247d045429b77d21')
sha256sums_aarch64=('54a3c502215ce0f2a07ae35624fed38fbd977a613f0d1366247d045429b77d21')


prepare () {
  # Moves content of the subfolder named pico-8 to src root
  mv pico-8/* .
  # Changes license and icon filenames to comply with naming conventions
  mv "license.txt" "LICENSE"
  mv "lexaloffle-pico8.png" "${pkgname}.png"
}


package () {
  local _name=pico8
  local _opt="${pkgdir}/opt/${pkgname}"
  local _share="${pkgdir}/usr/share"

  # Desktop entry
  install -Dm644 "${pkgname}.desktop" "${_share}/applications/${pkgname}.desktop"
  install -Dm644 "${pkgname}.png" "${_share}/pixmaps/${pkgname}.png"
  install -Dm644 "${pkgname}.xml" "${_share}/mime/packages/${pkgname}.xml"
  # License
  install -Dm644 "LICENSE" "${_share}/licenses/${pkgname}/LICENSE"
  # Data and readmes
  install -Dm644 -t "${_opt}" "${_name}.dat" "${pkgname}_manual.txt" readme_*.txt

  # Binary
  local _target
  case $CARCH in
    "x86_64" | "armv7h")
      _target="${_name}_dyn"
      ;;
    "i686")
      _target="${_name}_32bit_dyn"
      ;;
    "aarch64")
      _target="${_name}_64"
      ;;
  esac
  install -Dm755 "${_target}" "${_opt}/${_name}"

  # Links the installed binary to /usr/bin
  local _bin="${pkgdir}/usr/bin"
  mkdir -p "${_bin}"
  ln -s "/opt/${pkgname}/${_name}" "${_bin}/${_name}"
}
