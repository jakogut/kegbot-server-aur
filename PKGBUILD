# Maintainer: Joseph Kogut <joseph.kogut@gmail.com>

pkgname=kegbot-server
pkgver=v1.2.3.r7.g4f510310
pkgrel=1
pkgdesc="Kegbot Server, the internet beer kegerator monitoring system."
arch=("i686" "x86_64")
url="https://github.com/Kegbot/$pkgname/blob/master/README.md"
license=('GPL-2.0')
depends=('python2' 'mysql-python' 'redis')
makedepends=('python2-virtualenv')
install=kegbot-server.install
source=("git+https://github.com/Kegbot/$pkgname"
	"kegbot-server.service"
	"kegbot-setup")

 md5sums=('SKIP'
         'c6404b2d8a743da0a7e6822d86f8f3ec'
         '0af5e5a4ae85fb26b41184df02fc8968') 

pkgver () {
	cd "$pkgname"
	git describe --long --tags | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}

prepare() {
	true
}

build() {
	cd "$pkgname"
	virtualenv2 ../kegbot-venv && . ../kegbot-venv/bin/activate
	pip install -e .
}

package() {
	mkdir -p $pkgdir/{etc,usr/share}/webapps/
	cp -rf kegbot-venv $pkgdir/usr/share/webapps/kegbot

	mkdir -p $pkgdir/usr/bin/
	ln -sf /usr/share/webapps/kegbot/bin/kegbot $pkgdir/usr/bin/kegbot
	install -m755 kegbot-setup $pkgdir/usr/bin/kegbot-setup

	mkdir -p $pkgdir/usr/lib/systemd/system/
	install -m644 kegbot-server.service $pkgdir/usr/lib/systemd/system/

	install -d -o kegbot -g kegbot -m 755 $pkgdir/etc/webapps/kegbot
	install -d -o kegbot -g kegbot -m 755 $pkgdir/var/lib/kegbot
}


