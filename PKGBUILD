# Maintainer: Piero Proietti <piero.proietti_at_gmail.com>

pkgname=penguins-eggs
pkgver=9.3.15 # autoupdate
pkgrel=1
pkgdesc="A terminal utility which allows you to remaster your system and redistribute it as an ISO image, on a USB stick or through the network via PXE remote boot"
arch=('any')
url='https://penguins-eggs.net'
license=('GPL2')

# from branch (develop)
_url="https://github.com/pieroproietti/penguins-eggs"
_branch="master"
source=("git+${_url}.git#branch=${_branch}")
sha256sums=('SKIP')
pkgver() {
	 cd ${srcdir}/${pkgname}
   grep 'version' package.json | awk 'NR==1 {print $2 }' | awk -F '"' '{print $2}'
   cd ..
   mv ${srcdir}/${pkgname} ${srcdir}/${pkgname}-${pkgver}
}

# from release
#source=("${pkgname}-${pkgver}.tar.gz"::"https://github.com/pieroproietti/${pkgname}/archive/v${pkgver}.tar.gz")
#sha256sums=('ea1468f54ad134f4dd91b84811a00668647627b00f9a26b43099418494ca70fb')

options=('!strip')
makedepends=('npm')
depends=('coreutils' 'cryptsetup' 'curl' 'dosfstools' 'dpkg-dev' 'git'
         'isolinux' 'live-boot' 'live-boot-initramfs-tools' 'lvm2' 
         'nodejs' 'parted' 'pxelinux' 'rsync' 'squashfs-tools' 'sshfs'
         'syslinux' 'syslinux-common' 'xorriso')
optdepends=('bash-completion: enable eggs commands automatic completion'
            'calamares: system installer GUI')

build() {
  cd "${pkgname}-${pkgver}"
  # Install pnpm into "pnpm-dir"
  #npm set prefix "pnpm-dir"
  #npm install -g pnpm
  # Build lib
  #pnpm-dir/bin/pnpm install
  #pnpm-dir/bin/pnpm build
  pnpm install
  pnpm build
}

package() {
  cd "${pkgname}-${pkgver}"

  # Fix permissions
  chown root:root "dist" "node_modules"
  # Fix paths for node modules
  find node_modules -type f -print0 | xargs --null sed -i "s#${srcdir}/${pkgname}-${pkgver}/#/usr/lib/eggs/#"

  install -m 755 -d "${pkgdir}/usr/lib/${pkgname}"
  cp -r -t "${pkgdir}/usr/lib/${pkgname}/" addons assets bin conf dist ipxe node_modules mkinitcpio pnpm-lock.yaml scripts
  install -m 644 -D package.json -t "${pkgdir}/usr/lib/${pkgname}/"

  # Install documentation
  install -m 755 -d "${pkgdir}/usr/share/doc/${pkgname}/"
  install -m 644 -D README.md "${pkgdir}/usr/share/doc/${pkgname}/"

  # Symlink executable
  install -m 755 -d "${pkgdir}/usr/bin"
  ln -s "/usr/lib/${pkgname}/bin/run" "${pkgdir}/usr/bin/eggs"

  # Install shell completion files
  install -m 755 -d "${pkgdir}/usr/share/bash-completion/completions"
  mv "${pkgdir}/usr/lib/${pkgname}/scripts/eggs.bash" "${pkgdir}/usr/share/bash-completion/completions/"
  install -m 755 -d "${pkgdir}/usr/share/zsh/functions/Completion/Zsh/"
  mv "${pkgdir}/usr/lib/${pkgname}/scripts/_eggs" "${pkgdir}/usr/share/zsh/functions/Completion/Zsh/"

  # Install man page
  install -m 644 -D manpages/doc/man/eggs.1.gz "${pkgdir}/usr/share/man/man1/eggs.1.gz"

  # Install desktop files
  install -m 644 -D "assets/${pkgname}.desktop" "${pkgdir}/usr/share/applications/${pkgname}.desktop"

  # Install icons
  install -m 644 -D assets/eggs.png -t "${pkgdir}/usr/share/pixmaps/"
}

