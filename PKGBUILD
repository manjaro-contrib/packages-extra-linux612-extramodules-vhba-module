# Maintainer: Philip Müller <philm[at]manjaro[dot]org>
# Maintainer: Bernhard Landauer <bernhard@manjaro.org>
# Contributor: Jan Alexander Steffens (heftig) <heftig@archlinux.org>
# Contributor: Ray Rashif <schiv@archlinux.org>
# Contributor: Mateusz Herych <heniekk@gmail.com>
# Contributor: Charles Lindsay <charles@chaoslizard.org>

_linuxprefix=linux612

_module=vhba-module
pkgname="${_linuxprefix}-${_module}"
pkgver=20260313
pkgrel=12
pkgdesc="Virtual SCSI adapter - Linux modules"
arch=('x86_64')
url="https://cdemu.sourceforge.io/"
license=('GPL-2.0-or-later')
depends=("${_linuxprefix}")
makedepends=("${_linuxprefix}-headers" "${_module}-dkms=$pkgver")
provides=("${_module}=$pkgver" "VHBA-MODULE")
groups=("${_linuxprefix}-extramodules")
options=(!debug !strip)

build() {
  _kernver="$(cat /usr/src/${_linuxprefix}/version)"
  fakeroot dkms build --dkmstree "$srcdir" -m "${_module}/$pkgver" -k "${_kernver}"
}

package() {
  _kernver="$(cat /usr/src/${_linuxprefix}/version)"
  _extramodules="/usr/lib/modules/${_kernver}/extramodules"
  install -Dm644 -t "${pkgdir}${_extramodules}" \
    "${_module}/$pkgver/${_kernver}/${CARCH}"/module/*.ko*

  # compress kernel modules
  find "$pkgdir" -name '*.ko' -exec zstd --rm -19 {} +
}
