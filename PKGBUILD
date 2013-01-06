# Maintainer: Gerald Dachs <gda[at]dachsweb[dot]de>
pkgname=vdr-dbus2vdr
pkgver=20130106
_vdrapi=1.7.35
pkgrel=1yavdr1
pkgdesc="controlling vdr via DBus as an alternative to SVDRP"
url="https://github.com/flensrocker/vdr-plugin-dbus2vdr"
arch=('x86_64' 'i686')
license=('GPL2')
depends=('gcc-libs' 'png++' "vdr-api=${_vdrapi}")
makedepends=('git')
optdepends=()
_plugname=$(echo $pkgname | sed 's/vdr-//g')
replaces=("vdr-plugin-$_plugname")
conflicts=("vdr-plugin-$_plugname")
#source=("git://github.com/flensrocker/vdr-plugin-dbus2vdr.git")
#md5sums=('SKIP')
_gitroot="git://github.com/flensrocker/vdr-plugin-dbus2vdr.git"
_gitname="vdr-plugin-dbus2vdr"

package() {
  cd "$srcdir"
  msg "Connecting to GIT server...."

  if [ -d $_gitname ] ; then
    cd $_gitname && git pull origin
    msg "The local files are updated."
  else
    git clone $_gitroot $_gitname
  fi

  msg "GIT checkout done or server timeout"

  cd "$srcdir/$_gitname"

#  patch -p1 -i ${srcdir}/makefile.diff

  mkdir -p $pkgdir/usr/lib/vdr/plugins
  make CFLAGS="$(pkg-config vdr --variable=cflags)" \
       CXXFLAGS="$(pkg-config vdr --variable=cxxflags)" \
       VDRDIR="/usr/include/vdr" \
       LIBDIR="$pkgdir/$(pkg-config vdr --variable=libdir)" \
       LOCALEDIR="$pkgdir/$(pkg-config vdr --variable=locdir)"
}

