# Maintainer: Eric Vidal <eric@obarun.org>
# based on the original https://projects.archlinux.org/svntogit/packages.git/tree/trunk?h=packages/upower
# 						Maintainer: Jan de Groot <jgc@archlinux.org>

pkgname=upower
pkgver=0.99.7
pkgrel=3
pkgdesc="Abstraction for enumerating power devices, listening to device events and querying history and statistics"
arch=('x86_64')
url="http://upower.freedesktop.org"
license=('GPL')
depends=('libusb' 'libimobiledevice' 'libgudev')
makedepends=('intltool' 'docbook-xsl' 'gobject-introspection' 'python2' 'git' 'gtk-doc')
backup=('etc/UPower/UPower.conf')
_commit=b443f750cfeee460323d8d9f214ff691345d01ef # tags/UPOWER_0_99_7^0
source=("git+https://anongit.freedesktop.org/git/upower#commit=$_commit")
md5sums=('SKIP')
validpgpkeys=('6DD4217456569BA711566AC7F06E8FDE7B45DAAC') # Eric Vidal

pkgver() {
  cd ${pkgname}
  git describe --tags | sed -e 's/UPOWER_//' -e 's/_/\./g' -e 's/-/+/g'
}

build() {
  cd ${pkgname}
   export PYTHONPATH="/usr/share/glib-2.0"
  NOCONFIGURE=1 ./autogen.sh
  
  ./configure \
    --prefix=/usr \
    --sysconfdir=/etc \
    --localstatedir=/var \
    --libexecdir=/usr/lib \
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
