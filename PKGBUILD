# Maintainer: Christian Weber <christianweber802 at gmx dot net>

pkgname=ndiswrapper
pkgver=1.59
pkgrel=9
epoch=
pkgdesc="Module for NDIS (Windows Network Drivers) drivers supplied by vendors."
arch=('i686' 'x86_64')
url="http://sourceforge.net/projects/ndiswrapper/"
license=('GPL')
depends=('linux>=3.18' 'linux<3.19')
makedepends=('linux-headers>=3.18' 'linux-headers<3.19')
optdepends=('ndisgtk: GTK+ based frontend for ndiswrapper.')
provides=('ndiswrapper')
install="ndiswrapper.install"
source=("http://download.sourceforge.net/ndiswrapper/$pkgname-$pkgver.tar.gz" "https://raw.githubusercontent.com/Schwartz/ndiswrapper-patch/master/ndiswrapper-1.59.patch")
md5sums=('e26a7213468ccd6b0bb4c211c7aadeaa'
         '8bc2bec85cfbd1a04d4038757fbc7829')

_EXTRAMODULES='extramodules-3.18-ARCH'
_KERNEL=$(cat /usr/lib/modules/${_EXTRAMODULES}/version)


prepare() {
	[ -z "$_KERNEL" ] && error "Could not get kernel version from '/usr/lib/modules/${_EXTRAMODULES}/version'..." && false
	msg "Found kernel version: $_KERNEL"
}

build() {
	cd "$srcdir/$pkgname-$pkgver"
	patch -p1 -i ../ndiswrapper-1.59.patch
	make -C driver KVERS_UNAME=${_KERNEL}
	make -C utils
}

package() {
	cd "$srcdir/$pkgname-$pkgver"
	make -C driver DESTDIR=${pkgdir} KVERS_UNAME=${_KERNEL} install
	make -C utils DESTDIR=${pkgdir} install
}
