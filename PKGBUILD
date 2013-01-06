# Maintainer: Gerald Dachs <gda[at]dachsweb[dot]de>
pkgname=vdr-dbus2vdr
pkgver=
_vdrapi=1.7.35
pkgrel=1yavdr1
pkgdesc="controlling vdr via DBus as an alternative to SVDRP"
url="https://github.com/flensrocker/vdr-plugin-dbus2vdr"
arch=('x86_64' 'i686')
license=('GPL2')
depends=('gcc-libs' 'systemd' "vdr-api=${_vdrapi}")
makedepends=('git')
optdepends=()
_plugname=$(echo $pkgname | sed 's/vdr-//g')
replaces=("vdr-plugin-$_plugname")
conflicts=("vdr-plugin-$_plugname")
source=("git://github.com/flensrocker/vdr-plugin-dbus2vdr.git")
md5sums=('SKIP')
_gitname="vdr-plugin-dbus2vdr"

pkgver() {
  cd "${srcdir}/${_gitname}"
  echo $(git describe --always | sed 's/-/./g')
  # for git, if the repo has no tags, comment out the above and uncommnet the next line:
  #echo "$(git shortlog | grep -c '\s\+').$(git describe --always)"
  # This will give you a count of the total commits and the hash of the commit you are on.
  # Useful if you're making a repository with git packages so that they can have sequential
  # version numbers. (Else a pacman -Syu may not update the package)
}

package() {
  cd "${srcdir}/${_gitname}"

#  patch -p1 -i ${srcdir}/makefile.diff

  mkdir -p $pkgdir/usr/lib/vdr/plugins
  make CFLAGS="$(pkg-config vdr --variable=cflags)" \
       CXXFLAGS="$(pkg-config vdr --variable=cxxflags)" \
       VDRDIR="/usr/include/vdr" \
       LIBDIR="$pkgdir/$(pkg-config vdr --variable=libdir)" \
       LOCALEDIR="$pkgdir/$(pkg-config vdr --variable=locdir)"
}

