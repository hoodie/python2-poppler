# $Id$
# Maintainer: Ray Rashif <schiv@archlinux.org
# Contributor: György Balló <ballogy@freestart.hu>
# Contributor: Hendrik Sollich <hendrik.sollich@tu-dresden.de>

pkgname=python2-poppler
_realname=pypoppler
pkgver=0.12.1
pkgrel=801
pkgdesc="Python 2.x bindings for Poppler (Hendriks Patch)"
arch=('i686' 'x86_64')
url="https://launchpad.net/poppler-python"
license=('GPL')
depends=('pygtk' 'poppler-glib' 'glib2' 'freetype2')
provides=('pypoppler' 'python-poppler')
conflicts=('python-poppler')
replaces=('python-poppler')
source=("http://launchpad.net/poppler-python/trunk/development/+download/$_realname-$pkgver.tar.gz"
        'pypoppler-0.12.1-poppler-0.16.0.patch'
        'additions.patch'
        )
md5sums=('1a89e5ed3042afc81bbd4d02e0cf640a'
         '683c5b67866d56adc2494120cc329dc8'
         '200a5c3308a35f559b580fd6d050cb1b'
         )

build() {
  cd "$srcdir/$_realname-$pkgver"

  # poppler 0.16 compat
  patch -Np0 -i \
	  "$srcdir/pypoppler-0.12.1-poppler-0.16.0.patch"

  # hendriks changes
  patch -Np0 -i \
	  "$srcdir/additions.patch"

  # poppler 0.18 compat
  sed -i "/pixbuf/,/^)/d" poppler.defs

  ./configure --prefix=/usr \
              --sysconfdir=/etc \
              --localstatedir=/var \
              --disable-static \
              PYTHON=python2
  make
}

package() {
  cd "$srcdir/$_realname-$pkgver"

  make DESTDIR="$pkgdir" install
}

# vim:set ts=2 sw=2 et:
