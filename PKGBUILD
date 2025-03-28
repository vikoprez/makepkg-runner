# Maintainer: Herobrine Persson <heropersson@protonmail.com>
# Contributor: Evan Goode <mail@evangoo.de>
# Contributor: Sefa Eyeoglu <contact@scrumplex.net>
# Contributor: txtsd <aur.archlinux@ihavea.quest>
# Contributor: seth <getchoo at tuta dot io>
# Contributor: fn2006 <usernamefn2006alreadyused@protonmail.com>
# Contributor: Lenny McLennington <lennymclennington@protonmail.com>
# Contributor: Elijah Gregg <lovetocode999@tilde.team>
# Contributor: Miko <mikoxyzzz@gmail.com>
# Contributor: Cheru Berhanu <aur attt cheru doot dev>
# Contributor: dada513 <dada513@protonmail.com>

pkgname=fjordlauncherunlocked
pkgver=9.2.4
pkgrel=1
pkgdesc="Prism Launcher fork with support for alternative auth servers"
arch=('i686' 'x86_64' 'aarch64')
url='https://github.com/hero-persson/FjordLauncherUnlocked'
license=('GPL-3.0-only AND LGPL-3.0-or-later AND LGPL-2.0-or-later AND Apache-2.0 AND MIT AND LicenseRef-Batch AND OFL-1.1')
depends=(
  glibc
  gcc-libs
  java-runtime
  libgl
  qt6-base
  qt6-5compat
  qt6-svg
  qt6-imageformats
  qt6-networkauth
  quazip-qt6
  zlib
  hicolor-icon-theme
  tomlplusplus
  cmark
)
provides=('fjordlauncher')
conflicts=('fjordlauncher')
makedepends=(cmake extra-cmake-modules git jdk17-openjdk scdoc ghc-filesystem gamemode)
optdepends=('glfw: to use system GLFW libraries'
            'openal: to use system OpenAL libraries'
            'visualvm: Profiling support'
            'xorg-xrandr: for older minecraft versions'
            'flite: minecraft voice narration')
source=("https://github.com/hero-persson/FjordLauncherUnlocked/releases/download/${pkgver}/FjordLauncher-${pkgver}.tar.gz")
b2sums=('c43d77bc2d4828fb9238e9115c3c7a00b36d7c72493f3962e18880c85214b353044f89473dd5db223df90c766f8ccb7dbe5a73ae3feb41406b370b5f7d69d6d3')

build() {
  cd FjordLauncher-$pkgver

  export PATH="/usr/lib/jvm/java-17-openjdk/bin/:$PATH"

  cmake -DCMAKE_BUILD_TYPE= \
    -DCMAKE_INSTALL_PREFIX="/usr" \
    -DLauncher_BUILD_PLATFORM="archlinux" \
    -DLauncher_QT_VERSION_MAJOR="6" \
    -Bbuild -S.
  cmake --build build
}

check() {
  cd FjordLauncher-$pkgver/build
  ctest .
}

package() {
  # licenses
  install -Dm644 lionshead.license -t "$pkgdir"/usr/share/licenses/$pkgname/
  install -Dm644 batch.license -t "$pkgdir"/usr/share/licenses/$pkgname/
  install -Dm644 mdi.license -t "$pkgdir"/usr/share/licenses/$pkgname/

  cd FjordLauncher-$pkgver/build
  DESTDIR="$pkgdir" cmake --install .

  mv "${pkgdir}/usr/share/mime/packages/modrinth-mrpack-mime.xml" \
     "${pkgdir}/usr/share/mime/packages/fjordlauncher-modrinth-mrpack-mime.xml"
}
