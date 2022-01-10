pkgname="st"
pkgver="0.8.5"
pkgrel="1"
pkgdesc="A simple virtual terminal emulator for X."
arch=("i686" "x86_64" "armv7h" "aarch64")
license=("MIT")
depends=("libxft")
url=https://st.suckless.org

prepare()
{
    cd "${srcdir}"
    make patch
}

build()
{
    cd "${srcdir}"
    make
}

package()
{
    cd "${srcdir}"
    make PREFIX=/usr DESTDIR="${pkgdir}" install
}
