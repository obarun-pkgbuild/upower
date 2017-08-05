# Maintainer: Eric Vidal <eric@obarun.org>
# based on the original https://projects.archlinux.org/svntogit/packages.git/tree/trunk?h=packages/upower
# 						Maintainer: Jan de Groot <jgc@archlinux.org>

pkgname=upower
pkgver=0.99.4+12+g402640b
pkgrel=2
pkgdesc="Abstraction for enumerating power devices, listening to device events and querying history and statistics"
arch=('x86_64')
url="http://upower.freedesktop.org"
license=('GPL')
depends=('libusb' 'libimobiledevice' 'libgudev')
makedepends=('intltool' 'docbook-xsl' 'gobject-introspection' 'python2' 'git' 'gtk-doc')
backup=('etc/UPower/UPower.conf')
_commit=402640bee016472bf61c7a4ad9e5fac9790ea1bf
source=(git://anongit.freedesktop.org/upower#commit=$_commit)
md5sums=('SKIP')
validpgpkeys=('6DD4217456569BA711566AC7F06E8FDE7B45DAAC') # Eric Vidal

pkgver() {
  cd ${pkgname}
  git describe --tags | sed -e 's/UPOWER_//' -e 's/_/\./g' -e 's/-/+/g'
}

build() {
  cd ${pkgname}
   
  NOCONFIGURE=1 ./autogen.sh
  
  ./configure \
    --prefix=/usr \
    --sysconfdir=/etc \
    --localstatedir=/var \
    --libexecdir=/usr/lib/$pkgname \
    --disable-static \
    --with-udevrulesdir=/usr/lib/udev/rules.d \
    --with-systemdsystemunitdir=no \
    --with-systemdutildir=no
  make
}

package() {
  cd ${pkgname}
  make DESTDIR="$pkgdir" install
}
