# Maintainer: Sonu Ishaq <sonuishaq67@gmail.com>
_pkgname=Deskreen
pkgname=deskreen
pkgver=1.0.3
pkgrel=1
pkgdesc="Turns any device with a web browser to a second screen for your computer"
arch=('any')
url="https://github.com/pavlobu/deskreen"
license=('AGPL3')
provides=(${pkgname})
conflicts=(${pkgname})
replaces=(${pkgname})
depends=()
makedepends=('coreutils')
backup=()
options=('!strip')
source=("${_pkgname}-${pkgver}.AppImage::https://github.com/pavlobu/${pkgname}/releases/download/v${pkgver//_/-}/${_pkgname}-${pkgver}.AppImage"
    "${pkgname}.desktop")
sha256sums=(
    '2a272a093410be378f588bc36f0dbb047affeac55358330362e867f7e521a8d6'  
    '9f7f814e5f9d540c2ea5c07a86e72096b0af1fee7d109b5659a4ac8da1a2cfaa'
)

prepare() {
    chmod u+x ${srcdir}/${_pkgname}-${pkgver}.AppImage

    ${srcdir}/${_pkgname}-${pkgver}.AppImage --appimage-extract
}

package() {
    find ${srcdir}/squashfs-root/locales/ -type d -exec chmod 755 {} +
    find ${srcdir}/squashfs-root/resources/ -type d -exec chmod 755 {} +

    install -d ${pkgdir}/opt/${pkgname}
    cp -r ${srcdir}/squashfs-root/* ${pkgdir}/opt/${pkgname}

    # remove broken or unused files and directories
    rm -r ${pkgdir}/opt/${pkgname}/usr/
    rm ${pkgdir}/opt/${pkgname}/AppRun
    rm ${pkgdir}/opt/${pkgname}/${pkgname}.desktop
    rm ${pkgdir}/opt/${pkgname}/${pkgname}.png

    find ${srcdir}/squashfs-root/usr/share/icons/ -type d -exec chmod 755 {} +

    install -d ${pkgdir}/usr/share/icons
    cp -r ${srcdir}/squashfs-root/usr/share/icons/hicolor ${pkgdir}/usr/share/icons/hicolor

    install -d ${pkgdir}/usr/bin
    ln -s ../../opt/${pkgname}/${pkgname} ${pkgdir}/usr/bin/${pkgname}

    install -Dm644 ${srcdir}/${pkgname}.desktop ${pkgdir}/usr/share/applications/${pkgname}.desktop
}
