pkgname=marvex
pkgver=20161206
pkgrel=1
pkgdesc="drop-in replacement for urxvt call"
arch=('i686' 'x86_64')
license=('GPL')
makedepends=('go' 'git')

source=(
	"marvex::git://github.com/reconquest/marvex.git"
)

md5sums=(
	'SKIP'
)

pkgver() {
	cd "$srcdir/$pkgname"
	git log -1 --format="%cd" --date=short | sed s/-//g
}

build() {
	cd "$srcdir/$pkgname"

	if [ -L "$srcdir/$pkgname" ]; then
		rm "$srcdir/$pkgname" -rf
		mv "$srcdir/.go/src/$pkgname/" "$srcdir/$pkgname"
	fi

	rm -rf "$srcdir/.go/src"

	mkdir -p "$srcdir/.go/src"

	export GOPATH="$srcdir/.go"

	mv "$srcdir/$pkgname" "$srcdir/.go/src/"

	cd "$srcdir/.go/src/$pkgname/"
	ln -sf "$srcdir/.go/src/$pkgname/" "$srcdir/$pkgname"

	echo "Running 'go get'..."
	go get
}

package() {
	install -DT "$srcdir/.go/bin/$pkgname" "$pkgdir/usr/bin/$pkgname"
}