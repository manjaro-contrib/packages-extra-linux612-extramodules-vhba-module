# Maintainer: Philip Müller <philm[at]manjaro[dot]org>
# Maintainer: Bernhard Landauer <bernhard@manjaro.org>
# Contributor: Jan Alexander Steffens (heftig) <heftig@archlinux.org>
# Contributor: Ray Rashif <schiv@archlinux.org>
# Contributor: Mateusz Herych <heniekk@gmail.com>
# Contributor: Charles Lindsay <charles@chaoslizard.org>

_linuxprefix=linux612

_module=vhba-module
pkgname="${_linuxprefix}-${_module}"
pkgver=20240202
pkgrel=0.1
pkgdesc="Kernel module that emulates SCSI devices"
arch=('x86_64')
url="https://cdemu.sourceforge.io/"
license=('GPL-2.0-or-later')
depends=("${_linuxprefix}")
makedepends=("${_linuxprefix}-headers")
provides=("${_module}=$pkgver" "VHBA-MODULE")
groups=("${_linuxprefix}-extramodules")
source=("http://downloads.sourceforge.net/cdemu/${_module}-$pkgver.tar.xz" kernel611.patch)
sha256sums=('bf5850d4b8f50221ca87d7343a929eda87b191f6f5ae8c614174543b5badde83'
            '18819f20bb432db7387fdffe1ff173ba4f2c91fb246b66f6da09684c5097dba6')

prepare() {
  cd "${_module}-$pkgver"
  patch -p2 -i ../kernel611.patch
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

  find "$pkgdir" -name '*.ko' -exec strip --strip-debug {} +
  find "$pkgdir" -name '*.ko' -exec xz {} +
}
