# This is an example PKGBUILD file. Use this as a start to creating your own,
# and remove these comments. For more information, see 'man PKGBUILD'.
# NOTE: Please fill out the license field for your package! If it is unknown,
# then please put 'unknown'.

# Maintainer: Mario Aichinger <aichingm@gmail.com>
_pkgname=pam-unix-others
pkgname="${_pkgname}-git"
pkgver=20200202042034
pkgrel=1
pkgdesc="PAM module to allow certain users to authenticate certain users"
arch=('i686' 'x86_64' 'arm' 'armv6h' 'armv7h' 'aarch64')
url="https://github.com/aichingm/pam_unix_others"
license=('GPLv2')
makedepends=('pam' 'git' 'make' 'autoconf')
source=("git+${url}")
md5sums=('SKIP')
install="${_pkgname}.install"
pkgver() {
  cd "$srcdir/${_pkgname}"
  date --date="$(git log -1 --date=iso --format=%cd)" "+%Y%m%d%H%M%S"
}

prepare() {
  mv pam_unix_others pam-unix-others
}

build() {
	cd "$srcdir/${_pkgname}"
  ./autogen.sh
	./configure \
      --prefix=/usr \
      helper=unix_others_chkpwd \
      module=pam_unix_others.so \
      process_group=can_puo \
      user_group=allow_puo # --enable-debugging
	make 
}

check() {
  echo pass
}

package() {
	cd "$srcdir/${_pkgname}"
	make PREFIX_BIN="${pkgdir}/usr/" PREFIX_LIB="${pkgdir}/usr/" install
}

