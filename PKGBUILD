# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Filipe Laíns (FFY00) <lains@archlinux.org>
# Maintainer: Daniel M. Capella <polyzen@archlinux.org>

_pkgname=installer
pkgname=python-$_pkgname
pkgver=0.7.0
pkgrel=8
pkgdesc='Low-level library for installing a Python package from a wheel distribution'
arch=('any')
url='https://github.com/pypa/installer'
license=('MIT')
depends=('python')
makedepends=(
  'git'
  'python-flit-core'
  'python-build'
)
checkdepends=(
  'python-pytest'
)
source=(
  "$pkgname-$pkgver.tar.gz::$url/archive/refs/tags/$pkgver.tar.gz"
)
sha512sums=(
  'a509c6ea9d88b8527cce0428ca6109077820cb9aa352967a389012bac40f8ec04039ab73710f4fb32b32ed20affd520ce0ba16ba18d9d380ce0af1f51fe8e2c6'
)

build() {
  cd \
    "${_pkgname}-${pkgver}"
  "${_py}" \
    -m \
      build \
      -wn \
      --skip-dependency-check
}

check() {
  cd \
    "${_pkgname}-${pkgver}"
  PYTHONPATH=src \
    pytest
}

package() {
  cd \
    "${_pkgname}-${pkgver}"
  PYTHONPATH=src \
    "${_py}" \
      -m installer \
      --destdir="${pkgdir}" \
      dist/*.whl
  # remove windows entrypoint scripts executables
  rm \
    "${pkgdir}/usr/lib/python"*"/site-packages/installer/_scripts/"*".exe"
  install \
    -Dm644 \
    LICENSE \
    "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
