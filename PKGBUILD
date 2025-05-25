# Maintainer: matteodev <me@matteodev.xyz>
# shellcheck disable=all

pkgname=jdk8-temurin
_majorver=8
_jdkver=8u452-b09
_jvmdir=/usr/lib/jvm/java-${_majorver}-temurin
_majorver=8
pkgver=${_jdkver//-/}
pkgrel=1
pkgdesc="Temurin (OpenJDK ${_majorver} Java binaries by Adoptium, formerly AdoptOpenJDK)"
arch=('x86_64')
url="https://adoptium.net/"
license=('custom')
depends=('java-runtime-common>=3' 'java-environment-common' 'ca-certificates-utils' 'desktop-file-utils' 'libxrender' 'libxtst' 'alsa-lib')
options=('!strip') # Disable stripping of binaries
source=("https://mirrors.nju.edu.cn/adoptium/${_majorver}/jdk/x64/linux/OpenJDK${_majorver}U-jdk_x64_linux_hotspot_${pkgver}.tar.gz")
sha256sums=('9448308a21841960a591b47927cf2d44fdc4c0533a5f8111a4b243a6bafb5d27')
replaces=("jdk${_majorver}-adoptopenjdk")                              # Replaces the old 'jdk8-adoptopenjdk' package
install=install_jdk${_majorver}-temurin.sh                             # Script to be executed after package installation
provides=("java-environment=${_majorver}" "java-runtime=${_majorver}") # Provides the 'java-environment=8' and 'java-runtime=8' virtual packages

package() {
  # Grab all contents of downloaded tar and extract to correct places
  install -dm 755 "${pkgdir}${_jvmdir}"
  cp -ar "${srcdir}/jdk${_jdkver}/." "${pkgdir}${_jvmdir}"

  # License
  install -Dm644 ${srcdir}/jdk${_jdkver}/LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"

  # Man pages
  cd "${pkgdir}${_jvmdir}"
  for f in man/man1/* man/ja/man1/* man/ja_JP.UTF-8/man1/*; do
    install -Dm 644 "${f}" "${pkgdir}/usr/share/${f/\.1/-temurin${_majorver}.1}"
  done
}
