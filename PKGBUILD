# Maintainer: Joseph Kogut <joseph.kogut@gmail.com>

pkgname=kegbot-server
pkgver=v1.2.3.r7.g4f510310
pkgrel=1
pkgdesc="Kegbot Server, the internet beer kegerator monitoring system."
arch=("i686" "x86_64")
url="https://github.com/Kegbot/$pkgname/blob/master/README.md"
license=('GPL2')
depends=('python2' 'mysql-python' 'redis' 'libjpeg' 'libtiff')
makedepends=('python2-virtualenv')
install=kegbot-server.install
source=("git+https://github.com/Kegbot/$pkgname"
	"kegbot-server.service"
	"kegbot-setup"
	"kegbot")

md5sums=('SKIP'
         '85ab2ed3906ff582a06fc02f300e72d0'
         '9b38001dd63da2794168e529e111bcd7'
         '16a9b746f2be7bfc870d9b86872e395a')

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
	python setup.py install
	pip install pillow
}

package() {
	mkdir -p $pkgdir/usr/share/webapps/
	cp -rf kegbot-venv $pkgdir/usr/share/webapps/kegbot

	mkdir -p $pkgdir/usr/bin/
	ln -sf /usr/share/webapps/kegbot/bin/kegbot $pkgdir/usr/bin/kegbot
	install -m755 kegbot-setup $pkgdir/usr/bin/kegbot-setup
	install -m755 kegbot $pkgdir/usr/bin/kegbot

	mkdir -p $pkgdir/usr/lib/systemd/system/
	install -m644 kegbot-server.service $pkgdir/usr/lib/systemd/system/
}


