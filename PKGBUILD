# Maintainer: Adis Hamzić <adis (at) hamzadis (dot) com>
_pkgname=digistump-arduino
pkgname=${_pkgname}-git
pkgver=20150119
pkgrel=1
pkgdesc="Files to add Digistump support (Digispark, Pro, DigiX) to Arduino 1.5.X (1.5.8+)"
arch=('i686' 'x86_64')
url="https://github.com/digistump/DigistumpArduino"
license=('GPL')
depends=('arduino-beta' 'micronucleus-cli-git')
makedepends=('git')
options=('!strip')
provides=(${_pkgname})
conflicts=(${_pkgname})
source=('git+https://github.com/digistump/DigistumpArduino')
sha256sums=('SKIP')

[ "$CARCH" = "i686" ] && _binaries='linux32binaries.tar'
[ "$CARCH" = "x86_64" ] && _binaries='linux64binaries.tar'

pkgver() {
  cd "${srcdir}/DigistumpArduino"
  git log -1 --format='%cd' --date=short | tr -d -- '-'
}

package() {
  cd "${srcdir}/DigistumpArduino"

  # base directory
  dest="${pkgdir}/usr/share/arduino/hardware/digistump"
  mkdir -p "${dest}"

  # copy all files, remove .exe files
  cp -r "hardware/digistump"/* "${dest}"
  find "${dest}" -iname "*.exe" -exec rm '{}' ';'

  # extract the correct tar archive
  cd "${dest}/avr/tools"
  tar -xf "${_binaries}"
  rm *.tar

  # wrong micronucleus is shipped, remove it
  rm micronucleus

  # use the micronucleus-cli version
  ln -s /usr/bin/micronucleus .
}

