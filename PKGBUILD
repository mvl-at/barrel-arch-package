# Maintainer: Richard Stöckl <richard.stoeckl@aon.at>

pkgname=barrel-git
pkgver=1788686b
pkgrel=1
pkgdesc="backend of the Musikverein Leopoldsdorf"
arch=('any')
url="https://github.com/mvl-at/barrel"
license=('GPL2')
provides=('barrel')
depends=('java-runtime>=16')
makedependens=('git' 'java-environment>=16')
source=('git+http://github.com/mvl-at/barrel.git'
        'barrel.service' 
        'barrel.sysusers')
sha256sums=('SKIP'
            'SKIP'
            'SKIP')

backup=('etc/barrel/barrel.yml')

pkgver() {
  cd "${srcdir}/barrel"
  git rev-parse HEAD | cut -c 1-8
}

build() {
  cd "${srcdir}/barrel"
  rm -rf "${srcdir}"/barrel/build/libs/barrel*.jar
  ./gradlew bootJar
}

package() {
  install -Dm744 -o 926 "${srcdir}"/barrel/build/libs/barrel*.jar "${pkgdir}/usr/share/barrel/barrel.jar"
  install -Dm600 -o 926 "${srcdir}/barrel/src/main/resources/application.yml" "${pkgdir}/etc/barrel/barrel.yml"

  install -Dm644 "${srcdir}/barrel.sysusers" "${pkgdir}/usr/lib/sysusers.d/barrel.conf"
  install -Dm644 "${srcdir}/barrel.service" -t "${pkgdir}/usr/lib/systemd/system"
}
