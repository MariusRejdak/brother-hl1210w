# Maintainer: wmax641 <spam at wmax641 dot website>
# Contributor: Marius Rejdak <mariuswol at gmail dot com>
pkgname=brother-hl1210w
pkgver=3.0.1_1
pkgrel=3
pkgdesc='Driver for the Brother HL-1210W printer'
url='http://support.brother.com/g/b/downloadtop.aspx?c=gb&lang=en&prod=hl1210w_eu_as'
license=('custom:brother')
depends=('cups' 'ghostscript')
depends_x86_64=('lib32-glibc')
arch=('i686' 'x86_64')

md5sums=('49b496b65089f31917c974f8bcc9643c'
         '76db4e113a1186f86410146b2ea39166'
         '0d7c2ba3a1a30b5babd855efac48b1fb')

source=("brother-hl1210w.patch"
        "http://download.brother.com/welcome/dlf101549/hl1210wlpr-${pkgver/_/-}.i386.rpm"
        "http://download.brother.com/welcome/dlf101548/hl1210wcupswrapper-${pkgver/_/-}.i386.rpm")

build() {
    cd "$srcdir"
    patch -Np0 < brother-hl1210w.patch
}

package() {
    cp -R "$srcdir"/opt "$pkgdir"/opt

    install -d "$pkgdir"/usr/share/cups/model
    ln -s /opt/brother/Printers/HL1210W/cupswrapper/brother-HL1210W-cups-en.ppd "$pkgdir"/usr/share/cups/model

    install -d "$pkgdir"/usr/lib/cups/filter
    ln -s /opt/brother/Printers/HL1210W/cupswrapper/brother_lpdwrapper_HL1210W "$pkgdir"/usr/lib/cups/filter

    install -d "$pkgdir"/etc/opt/brother/Printers/HL1210W/inf
    ln -s /opt/brother/Printers/HL1210W/inf/brHL1210Wrc "$pkgdir"/etc/opt/brother/Printers/HL1210W/inf/

    install -d "$pkgdir"/usr/bin
    cat << EOF > "$pkgdir"/usr/bin/brprintconflsr3_HL1210W
#!/bin/sh
/opt/brother/Printers/HL1210W/lpd/brprintconflsr3 -P HL1210W $*
EOF
    chmod 755 "$pkgdir"/usr/bin/brprintconflsr3_HL1210W
}
