# Maintainer: Radioactiveman <thomas-lange2@gmx.de>
# Contributor: Jan de Groot <jgc@archlinux.org>

_pkgname=eog
pkgname=eog2
pkgver=2.32.1
pkgrel=1
pkgdesc="Eye of Gnome: An image viewing and cataloging program"
arch=('i686' 'x86_64')
license=('GPL')
depends=('gnome-desktop2' 'libexif>=0.6.19' 'lcms>=1.19' 'desktop-file-utils' 'gnome-icon-theme>=2.31.0' 'exempi>=2.1.1' 'python2>=2.7')
makedepends=('pkg-config' 'gnome-doc-utils>=0.20.1' 'intltool' 'pygtk')
conflicts=('eog')
install=$pkgname.install
options=('!emptydirs' '!libtool')
url="http://projects.gnome.org/eog/"
source=(http://ftp.gnome.org/pub/gnome/sources/$_pkgname/2.32/$_pkgname-$pkgver.tar.bz2)
sha256sums=('543672fb8e8e300bf2cf4c7eef43b5b1624e2e48e6aa0801a083ae7beb2d7078')

build() {
    cd "${srcdir}/${_pkgname}-${pkgver}"

    LDFLAGS+=' -Wl,--copy-dt-needed-entries'

    PYTHON=python2 ./configure \
        --prefix=/usr \
        --sysconfdir=/etc \
        --localstatedir=/var \
        --disable-scrollkeeper \
        --enable-python
    make
}

package() {
    cd "${srcdir}/${_pkgname}-${pkgver}"
    make GCONF_DISABLE_MAKEFILE_SCHEMA_INSTALL=1 DESTDIR="${pkgdir}" install

    install -m755 -d "${pkgdir}/usr/share/gconf/schemas"
    gconf-merge-schema "${pkgdir}/usr/share/gconf/schemas/${_pkgname}.schemas" --domain eog ${pkgdir}/etc/gconf/schemas/*.schemas
    rm -f ${pkgdir}/etc/gconf/schemas/*.schemas
}
