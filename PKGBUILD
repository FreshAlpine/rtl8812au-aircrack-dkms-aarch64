# Maintainer: tmikey <mike at tmikey dot tech>

# based on rtl8812au-aircrack-ng

_pkgname=rtl8812au
_commit="60f74eb102fc29b6f3f0388c9179f08563484bf2"
_main_ver="5.7.0"
pkgname=$_pkgname-aircrack-dkms-aarch64
_diff_file=$pkgname.diff
pkgver=5.7.0.r1077.60f74eb
pkgrel=1
pkgdesc="Realtek rtl8812au (patched for aarch64, O3, mcpu=native, DFS)"
arch=('aarch64')
url="https://github.com/aircrack-ng/rtl8812au.git"
license=('GPL2')
depends=('dkms' 'bc')
makedepends=('git')
provides=("$_pkgname")
conflicts=("$_pkgname")
install=$pkgname.install
source=("$_pkgname::git+$url#commit=$_commit"
        "$_diff_file"
        'dkms.conf')
sha256sums=('SKIP'
            '14363a30a47d11b2579abcb303bcd64d8e6a565d2d7c7773608b89cd3e864c06'
            '1737cd581b75c8cda1987cc0957099bb257fe15669338626bd105cf0a69605b8')

pkgver() {
  cd "$_pkgname"
  printf "$_main_ver.r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare() {
  cd "$_pkgname"
  patch -p1 -i "$srcdir/$_diff_file"
  cp $srcdir/dkms.conf ./
  git add -u
  git add dkms.conf
}

package() {
  cd "$_pkgname"
  _installdir="$pkgdir/usr/src/$pkgname-$pkgver"
  mkdir -p "$_installdir"
  git checkout-index -a -f --prefix=$_installdir/

  install -Dm644 "$srcdir/dkms.conf" "$_installdir"

  sed -e "s/@PKGNAME@/$pkgname/" -e "s/@PKGVER@/$pkgver/" -i "$_installdir/dkms.conf"
}

# vim:set ts=2 sw=2 et:
