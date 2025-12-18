# Maintainer: Philip Müller <philm[at]manjaro[dot]org>
# Maintainer: Bernhard Landauer <bernhard@manjaro.org>
# Contributor: Jan Alexander Steffens (heftig) <heftig@archlinux.org>
# Contributor: Ray Rashif <schiv@archlinux.org>
# Contributor: Mateusz Herych <heniekk@gmail.com>
# Contributor: Charles Lindsay <charles@chaoslizard.org>

_linuxprefix=linux612

_module=vhba-module
pkgname="${_linuxprefix}-${_module}"
pkgver=20250329
pkgrel=51
pkgdesc="Kernel module that emulates SCSI devices"
arch=('x86_64')
url="https://cdemu.sourceforge.io/"
license=('GPL-2.0-or-later')
depends=("${_linuxprefix}")
makedepends=("${_linuxprefix}-headers")
provides=("${_module}=$pkgver" "VHBA-MODULE")
groups=("${_linuxprefix}-extramodules")
source=("http://downloads.sourceforge.net/cdemu/${_module}-$pkgver.tar.xz")
sha256sums=('a62a20d720ddf0cfe5a53228f4513d498d89c2ead9e9af0b1b6959ff8126075e')

prepare() {
  cd "${_module}-$pkgver"
}

build() {
  _kernver="$(cat /usr/src/${_linuxprefix}/version)"

  cd "${_module}-$pkgver"
  make KERNELRELEASE="${_kernver}"
}

package() {
  _kernver="$(cat /usr/src/${_linuxprefix}/version)"

  cd "${_module}-$pkgver"
  install -Dm644 *.ko -t "$pkgdir/usr/lib/modules/${_kernver}/extramodules/"

  find "$pkgdir" -name '*.ko' -exec zstd --rm -19 {} +
}
