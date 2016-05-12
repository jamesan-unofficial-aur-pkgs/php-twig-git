# Maintainer: James An <james@jamesan.ca>
# Contributor: Bruno Galeotti <bgaleotti@gmail.com>
# Forked from https://aur.archlinux.org/php-twig.git on commit 48ff4b1c.

pkgname=php-twig-git
_pkgname=${pkgname%-git}
__pkgname=${_pkgname#php-}
__pkgname=${__pkgname^}
pkgver=1.23.1.r14.gdba78c8
pkgrel=1
pkgdesc='PHP Twig extension.'
url="http://github.com/twigphp/$__pkgname"
license='BSD'
arch=('any')
depends=('php')
makedepends=('git')
provides=("$_pkgname=$pkgver")
conflicts=("$_pkgname")
source=("$__pkgname"::"git+https://github.com/twigphp/$__pkgname.git"
        "${__pkgname,}.ini")
backup=('etc/php/conf.d/${_pkgname,}.ini')
md5sums=('SKIP'
         '060537663d7f7984d07e2855595d3b54')

pkgver() {
  cd "$__pkgname"
  (
    set -o pipefail
    git describe --long --tag | sed -r 's/([^-]*-g)/r\1/;s/-/./g;s/^v//' ||
    printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
  )
}

build() {
  cd "$__pkgname/ext/${__pkgname,}"

  phpize
  ./configure --prefix=/usr "--enable-${__pkgname,}"
  make
}

package() {
  cd "$__pkgname"

  install -Dm755 "../${__pkgname,}.ini" "$pkgdir/etc/php/conf.d/${__pkgname,}.ini"
  install -Dm755 "ext/${__pkgname,}/modules/${__pkgname,}.so" "$pkgdir/usr/lib/php/modules/${__pkgname,}.so"
  install -Dm755 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
