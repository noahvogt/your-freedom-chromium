# Maintainer: Parabola Project <dev@lists.parabola.nu>

pkgname=your-freedom
pkgdesc="This package conflicts with every nonfree package known to date to ensure your system is free."
license=('GPL3')
url="https://git.parabola.nu/blacklist.git"
pkgver=20211018.1
_gitver=e3eeb82dc48d248e18ff240e778d77b765b336ce
pkgrel=1

arch=('any')
install=${pkgname}.install

makedepends=(librelib)
source=(blacklist-${_gitver}.txt::https://git.parabola.nu/blacklist.git/plain/blacklist.txt?id=${_gitver})
sha512sums=('e93f5f1476068a261ff84b2a07d222fd09587ac97adae0236e309d3a72a26b47421e99aabfebef8029c1c24449634e274996a548e0db6eb16e67f08795a56084')


package() {
	cd "$srcdir"

    sed -i '/^chromium*/d' "blacklist-${_gitver}.txt"

	conflicts=($( \
		< blacklist-${_gitver}.txt \
		libreblacklist normalize | \
		cut -d: -f1,2 | \
		sed -n 's/:$//p' | \
		sort -u \
		))

	install -Dm644 blacklist-${_gitver}.txt "$pkgdir"/usr/share/doc/${pkgname}/blacklist.txt
}
