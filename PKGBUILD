# Maintainer: tmikey <mike at tmikey dot tech>

# based on rtl8812au-aircrack-ng

_pkgname=rtl8812au
_commit="65174c4ded74b2da982a13605db59bc0b643c187"
_main_ver="5.6.4.2"
pkgname=$_pkgname-aircrack-dkms-aarch64
_diff_file=$pkgname.diff
pkgver=5.6.4.2.r999.65174c4
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
         '27fd29d8f0e6b3eeeb05aa8a75bedc00d0a250f2403975e65654f7223f384c08'
         'f3a686f378a66463b6702ba9e771c66959bb478cab61f7d3c214c2bdf5ec8e80')

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
