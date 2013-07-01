# Maintainer: Dalton Miller
# Contributor: Kilian Lackhove kilian@lackhove.de
pkgname=bittorrent-sync
pkgver=1.1.22
pkgrel=1
epoch=1
pkgdesc="BitTorrent Sync"
arch=('i686' 'x86_64' 'arm' 'armv6h')
url="http://labs.bittorrent.com/experiments/sync.html"
license=('custom')
backup=("etc/btsync.conf")
install="${pkgname}.install"
source=("bittorrent-sync.install"
	"btsync.service")
sha256sums=('b2240a8356c24356ca83bc2f9dcf759ceaa7dcdbbec45f5cc8cd0928b8f89df5'
	    '3ccf1a7e3f066bf4453035cbb5b4956b6d69d6abd4c41f34ed36b84f345ae90f')

if [ "$CARCH" == x86_64 ]; then
	source+=("http://syncapp.bittorrent.com/$pkgver/btsync_x64-$pkgver.tar.gz")
	sha256sums+=('1e202f5edc7dd9fbf4abdabe62f28f9bdb7aec803c17410cc2d8d9e7dfcd9123')
elif [ "$CARCH" == i686 ]; then
	source+=("http://syncapp.bittorrent.com/$pkgver/btsync_i386-$pkgver.tar.gz")
        sha256sums+=('abedcc3c0ba971250ec43abf3a4cafdf812bf1796f26c9a6beef3a4519645bdd')
elif [ "$CARCH" == arm ] || [ "$CARCH" == armv6h ]; then
        source+=("http://syncapp.bittorrent.com/$pkgver/btsync_arm-$pkgver.tar.gz")
        sha256sums+=('df4e11eb44286d1f46fcd6d055a65e8250e2a3543d9821f401019ccb265e806e')
fi

build() {
	cd "${srcdir}"
	./btsync --dump-sample-config > btsync.conf
}

package() {
	cd "${srcdir}"

	./btsync --dump-sample-config | sed 's:/home/user/\.sync:/var/lib/btsync:g' > btsync.conf
	install -D -m 644 btsync.conf "${pkgdir}/etc/btsync.conf"

	install -D -m 755 btsync "${pkgdir}/usr/bin/btsync"

	install -D -m 644 btsync.service "${pkgdir}/usr/lib/systemd/system/btsync.service"

	install -D -m 644 LICENSE.TXT "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE.TXT"
}
