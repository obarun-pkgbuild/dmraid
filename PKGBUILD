# Maintainer: Eric Vidal <eric@obarun.org>
# based on the original https://projects.archlinux.org/svntogit/packages.git/tree/trunk?h=packages/dmraid
# 						Maintainer: Tobias Powalowski <tpowa@archlinux.org>
# 						Contributor: Urs Wolfer <uwolfer @ fwo.ch>

pkgname=dmraid
pkgver=1.0.0.rc16.3
pkgrel=11
pkgdesc="Device mapper RAID interface"
url="http://people.redhat.com/~heinzm/sw/dmraid/"
conflicts=('mkinitcpio<0.7')
depends=('device-mapper>=2.0.54')
optdepends=('dmraid-s6rcserv: dmraid s6-rc service'
			'dmraid-runitserv: dmraid runit service')
arch=('x86_64')
license=('GPL')
source=(#https://sources.archlinux.org/other/dmraid/${pkgname}-$pkgver.tar.bz2
        http://people.redhat.com/~heinzm/sw/dmraid/src/${pkgname}-1.0.0.rc16-3.tar.bz2
        dmraid_install
        dmraid_hook)
install=$pkgname.install
md5sums=('819338fcef98e8e25819f0516722beeb'
         '7a040ebcba305aba1e47dfe6ca8323b5'
         'faec669dc85f87187b45b5d3968efe2c')
validpgpkeys=('6DD4217456569BA711566AC7F06E8FDE7B45DAAC') # Eric Vidal

build() {
  cd "${pkgname}/1.0.0.rc16-3/${pkgname}"
  ./configure --enable-led --enable-intel_led
  make
}

package() {
  cd "${pkgname}/1.0.0.rc16-3/${pkgname}"
  make DESTDIR="$pkgdir" sbindir=/usr/bin prefix=/usr libdir=/usr/lib mandir=/usr/share/man includedir=/usr/include install
  install -D -m644 "$srcdir"/dmraid_install "$pkgdir"/usr/lib/initcpio/install/dmraid
  install -D -m644 "$srcdir"/dmraid_hook "$pkgdir"/usr/lib/initcpio/hooks/dmraid
  

  # fix permissions
  chmod 644 "$pkgdir"/usr/include/dmraid/* "$pkgdir"/usr/lib/libdmraid.a
}
