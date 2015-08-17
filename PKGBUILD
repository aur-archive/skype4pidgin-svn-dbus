# Maintainer: Timothy Redaelli <timothy.redaelli@gmail.com>
# Contributor: DonVla <donvla@users.sourceforge.net>

pkgname=skype4pidgin-svn-dbus
pkgver=663
pkgrel=1
pkgdesc="Skype plugin for Pidgin and Empathy (with X11 and dbus support)"
arch=("i686" "x86_64")
url="http://skype4pidgin.googlecode.com/svn/trunk/"
license=('GPL3')
depends=('libpurple' 'skype')
makedepends=('pkg-config' 'subversion')
conflicts=('skype4pidgin' 'skype4pidgin-svn')
replaces=('skype4pidgin' 'skype4pidgin-svn')
source=("$pkgname::svn+http://skype4pidgin.googlecode.com/svn/trunk/"
        'Makefile.patch')
sha256sums=('SKIP'
            '26ed5c34f0ad9619aa0faff6ae210d61da7f9fd20d52fe9ea15b3c1941b52a3e')

pkgver() {
  cd "$pkgname"
  svnversion
}

build() {
  cd "$pkgname"

  patch -Np0 -i "$srcdir"/Makefile.patch
  sed -n -e 's/\[Skype\]/[Skype (D-Bus)]/' -e '/\[Skype (D-Bus)\]/,$p' theme >> theme

  make all
}

package() {
  cd "$pkgname"

  install -D -m 0755 libskype.so "${pkgdir}$(pkg-config --variable=plugindir purple)/libskype.so"
  install -D -m 0755 libskype_dbus.so "${pkgdir}$(pkg-config --variable=plugindir purple)/libskype_dbus.so"

  install -D -m 0644 icons/16/skype.png "${pkgdir}"/usr/share/pixmaps/pidgin/protocols/16/skype.png
  install -D -m 0644 icons/22/skype.png "${pkgdir}"/usr/share/pixmaps/pidgin/protocols/22/skype.png
  install -D -m 0644 icons/48/skype.png "${pkgdir}"/usr/share/pixmaps/pidgin/protocols/48/skype.png
  install -D -m 0644 theme "${pkgdir}"/usr/share/pixmaps/pidgin/emotes/skype/theme
}
