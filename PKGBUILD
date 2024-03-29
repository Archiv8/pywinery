#!/bin/bash

# Disable various shellcheck rules that produce false positives in this file.
# Repository rules should be added to the .shellcheckrc file located in the
# repository root directory, see https://github.com/koalaman/shellcheck/wiki
# and https://archiv8.github.io for further information.
# shellcheck disable=SC2034,SC2154
# ToDo: Add files: User documentation
# ToDo: Add files: Tooling
# FixMe: Namcap warnings and errors

# Maintainer: Ross Clark <archiv8@artisteducator.com>
# Contributor: Ross Clark <archiv8@artisteducator.com>



pkgname=pywinery
pkgver=0.3.3
pkgrel=3
pkgdesc="Graphical and simple wine-prefix manager which allows you to launch apps and manage configuration of separate prefixes."
license=(
	"GPL3"
	)
url="https://github.com/ergoithz/pywinery"
arch=(
	"any"
	)
makedepends=(
	"python-setuptools"
	)
depends=(
	"python" 
	"python-gobject>=3.4" 
	"gtk3" "xdg-utils"
	 "icoutils" 
	 "librsvg"
	 )
optdepends=(
	"winetricks: Install various redistributable runtime libraries in Wine"
	"wine: System wine version"
)
install="pywinery.install"
source=(
	"https://github.com/ergoithz/pywinery/releases/download/0.3.3/pywinery_0.3-3.tar.gz"
	"patch-gtk-version.patch"
)
sha512sums=(
	"ed2d5c103fa5a9fb8253532b66c718aee3c64d6c6488872322448731554033f5"
	"2241f5871227befd56238499f2ea459f9f7d013c871aea95edf8419cb98c6245"
)

prepare() {

	# Patch loading of gtk to ensure gtk3 is loaded
	patch --directory="${srcdir}/${pkgver%.*}" --forward --strip=1 --input="${srcdir}/patch-gtk-version.patch"
}

build() {

	cd ${srcdir}/${pkgver%.*}

	python setup.py build
}

package() {

	cd ${srcdir}/${pkgver%.*}

	python setup.py install --root="${pkgdir}" --optimize=1

	# Move app icon to proper folder
	install -D -m644 ${pkgdir}/usr/share/pywinery/pywinery.svg ${pkgdir}/usr/share/icons/hicolor/scalable/apps/pywinery.svg
	rm ${pkgdir}/usr/share/pywinery/pywinery.svg
}
