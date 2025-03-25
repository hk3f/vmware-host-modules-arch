#PKGEXT=.pkg.tar
pkgname=vmware-module-update
pkgver=17.6.3
_buildver=24583834
_pkgver=${pkgver}_${_buildver}
pkgrel=2
pkgdesc='Vmware workstation module update after linux kernel updated.'
arch=(x86_64)
url='https://www.vmware.com/products/workstation-for-linux.html'
license=(custom)
install="vmware-module-only.install"
conflicts=(
  vmware-modules-dkms
  vmware-ovftool
  vmware-patch
  vmware-systemd-services
)
provides=(
  vmware-ovftool
)
depends=(
  dkms
  fuse2
  gtkmm3
  libcanberra
  libaio
  pcsclite
  hicolor-icon-theme
  libxcrypt-compat # needed for ovftool
  # needed to use Arch GTK3 library (for theme integration)
  gtk3
  gcr
)
optdepends=(
  'linux-headers: build modules against Arch kernel'
)
makedepends=(
  sqlite
)
backup=(
  'etc/vmware/config'
  'etc/conf.d/vmware'
)
source=( 
  )
sha256sums=(
  )
options=(!strip emptydirs !debug)

package() {
  # Patch up the VMware kernel sources and configure DKMS.
  dkms_dir="$pkgdir"
echo "$srcdir"
  install -Dm 644 "$srcdir/Makefile" "$dkms_dir/Makefile"
  install -Dm 644 "$srcdir/dkms.conf.in" "$dkms_dir/dkms.conf"
  cd "$srcdir"
  sed \
    -e "s/@PKGNAME@/$pkgname/g" \
    -e "s/@PKGVER@/$_pkgver/g" \
    -i "$dkms_dir/dkms.conf"

  for module in vmmon vmnet; do
    tar -xf "$module.tar" -C "$dkms_dir"
    msg "Patching $module module for DKMS"
    patch -p2 --read-only=ignore --directory="$dkms_dir/$module-only" < "$srcdir/$module.patch"
  done
}
