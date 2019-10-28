# Maintainer: David Spink <yorper_protonmail.com>

# Based on the file created for Arch Linux by:
# Christian Hesse <mail@eworm.de>
# Tobias Powalowski <tpowa@archlinux.org>
# Ronald van Haren <ronald.archlinux.org>
# Keshav Padram <the.ridikulus.rat.gmail.com>

## "1" to enable IA32-EFI build in Arch x86_64, "0" to disable
_IA32_EFI_IN_ARCH_X64="1"

## "1" to enable EMU build, "0" to disable
_GRUB_EMU_BUILD="0"

_GRUB_INT_VER="2.04"
_GRUB_EXTRAS_COMMIT="136763a4cc9ca3a4f59d05b79eede2159d6f441e"
_GNULIB_COMMIT="9ce9be2ef0cb1180e35dfe9dfbbe90d774b374bd"
_UNIFONT_VER="12.1.02"

[[ "${CARCH}" == "x86_64" ]] && _EFI_ARCH="x86_64"
[[ "${CARCH}" == "i686" ]] && _EFI_ARCH="i386"

[[ "${CARCH}" == "x86_64" ]] && _EMU_ARCH="x86_64"
[[ "${CARCH}" == "i686" ]] && _EMU_ARCH="i386"

pkgname='grub'
pkgdesc='GNU GRand Unified Bootloader (2)'
_pkgver=2.04
pkgver=${_pkgver/-/}
pkgrel=5
url='https://www.gnu.org/software/grub/'
arch=('x86_64')
license=('GPL3')
backup=('etc/default/grub'
        'etc/grub.d/40_custom'
        'boot/grub/grub.cfg')
install="${pkgname}.install"
options=('!makeflags')

conflicts=('grub-common' 'grub-bios' 'grub-emu' "grub-efi-${_EFI_ARCH}" 'grub-legacy'
           'grub-fedora' 'grub-quiet-fedora' 'grub-quiet' 'grub-clean')
replaces=('grub-common' 'grub-bios' 'grub-emu' "grub-efi-${_EFI_ARCH}" 'grub-quiet' 'grub-clean')
provides=('grub-common' 'grub-bios' 'grub-emu' "grub-efi-${_EFI_ARCH}"
          "grub=$pkgver-$pkgrel")

makedepends=('git' 'rsync' 'xz' 'freetype2' 'ttf-dejavu' 'python' 'autogen'
             'texinfo' 'help2man' 'gettext' 'device-mapper' 'fuse2')
depends=('sh' 'xz' 'gettext' 'device-mapper')
optdepends=('freetype2: For grub-mkfont usage'
            'fuse2: For grub-mount usage'
            'dosfstools: For grub-mkrescue FAT FS and EFI support'
            'efibootmgr: For grub-install EFI support'
            'libisoburn: Provides xorriso for generating grub rescue iso using grub-mkrescue'
            'os-prober: To detect other OSes when generating grub.cfg in BIOS systems'
            'mtools: For grub-mkrescue FAT FS support')

if [[ "${_GRUB_EMU_BUILD}" == "1" ]]; then
    makedepends+=('libusbx' 'sdl')
    optdepends+=('libusbx: For grub-emu USB support'
                 'sdl: For grub-emu SDL support')
fi

validpgpkeys=('E53D497F3FA42AD8C9B4D1E835A93B74E82E4209'  # Vladimir 'phcoder' Serbinenko <phcoder@gmail.com>
              'BE5C23209ACDDACEB20DB0A28C8189F1988C2166'  # Daniel Kiper <dkiper@net-space.pl>
              '95D2E9AB8740D8046387FD151A09227B1F435A33') # Paul Hardy <unifoundry@unifoundry.com>

source=("git+https://git.savannah.gnu.org/git/grub.git#tag=grub-${_pkgver}?signed"
        "git+https://git.savannah.gnu.org/git/grub-extras.git#commit=${_GRUB_EXTRAS_COMMIT}"
        "git+https://git.savannah.gnu.org/git/gnulib.git#commit=${_GNULIB_COMMIT}"
        "https://ftp.gnu.org/gnu/unifont/unifont-${_UNIFONT_VER}/unifont-${_UNIFONT_VER}.bdf.gz"{,.sig}
        'grub-export-path.patch'
        'grub-add-GRUB_COLOR_variables.patch'
        'grub-cleanjaro-modifications.patch'
        'grub-use-efivarfs.patch'
        'background.png'
        'grub.default'
        'grub.cfg'
        'update-grub'
        "${pkgname}.hook")

sha256sums=('SKIP'
            'SKIP'
            'SKIP'
            '04d652be1e28a6d464965c75c71ac84633085cd0960c2687466651c34c94bd89'
            'SKIP'
            '63c611189a60d68c6ae094f2ced91ac576b3921b7fd2e75a551c2dc6baefc35e'
            'a5198267ceb04dceb6d2ea7800281a42b3f91fd02da55d2cc9ea20d47273ca29'
            '5cb8d4f590a2b61599efa3749df0e8584b7ceb37b9d5cb030c7dc6261f5d0aba'
            '20b2b6e7f501596b5cce6ffa05906980427f760c03d308d0e045cf2ecf47bb0e'
            '50108fd7a73885bb17f72483cb59a049350b19cad6c8bdbf2a7d0e85c6b6b500'
            'cd398373c76c78b177cb2a00c7173ed027b0410b22c5c1b087e4f13f9f8df5c6'
            '7fc95d49c0febe98a76e56b606a280565cb736580adecf163bc6b5aca8e7cbd8'
            '467b0101154076fee99d9574a5fb6b772a3923cc200a1f4ca08fe17be8d68111'
            '1488d7f3924bd7385a222e3e9685cdb1ecb39f3d6f882da6b5907b898f5b8f08')

_backports=(
)

_configure_options=(
	FREETYPE="pkg-config freetype2"
	BUILD_FREETYPE="pkg-config freetype2"
	--enable-mm-debug
	--enable-nls
	--enable-device-mapper
	--enable-cache-stats
	--enable-grub-mkfont
	--enable-grub-mount
	--prefix="/usr"
	--bindir="/usr/bin"
	--sbindir="/usr/bin"
	--mandir="/usr/share/man"
	--infodir="/usr/share/info"
	--datarootdir="/usr/share"
	--sysconfdir="/etc"
	--program-prefix=""
	--with-bootdir="/boot"
	--with-grubdir="grub"
	--disable-silent-rules
	--disable-werror
)

prepare() {
	cd "${srcdir}/grub/"

	echo "Apply backports..."
	local _c
	for _c in "${_backports[@]}"; do
		git log --oneline -1 "${_c}"
		git cherry-pick -n "${_c}"
	done

	# https://github.com/calamares/calamares/issues/918
	msg "Use efivarfs modules"
	patch -Np1 -i "${srcdir}/grub-use-efivarfs.patch"
	echo

	msg "Patch to export $PATH"
	patch -Np1 -i "${srcdir}/grub-export-path.patch"
	echo
	
	msg "Patch to enable GRUB_COLOR_* variables in grub-mkconfig"
	## Based on http://lists.gnu.org/archive/html/grub-devel/2012-02/msg00021.html
	patch -Np1 -i "${srcdir}/grub-add-GRUB_COLOR_variables.patch"
	echo

	msg "Patch to include Cleanjaro Linux Modifications"
	patch -Np1 -i "${srcdir}/grub-cleanjaro-modifications.patch"
	echo

        # delete line due man h2m
        sed -i -e '1369d' "Makefile.util.def"
	echo

	echo "Fix DejaVuSans.ttf location so that grub-mkfont can create *.pf2 files for starfield theme..."
	sed 's|/usr/share/fonts/dejavu|/usr/share/fonts/dejavu /usr/share/fonts/TTF|g' -i "configure.ac"

	echo "Fix mkinitcpio 'rw' FS#36275..."
	sed 's| ro | rw |g' -i "util/grub.d/10_linux.in"

	echo "Fix OS naming FS#33393..."
	sed 's|GNU/Linux|Linux|' -i "util/grub.d/10_linux.in"

	msg "Bump Version to ${pkgver}"
	sed -i -e "s|${_GRUB_INT_VER}|${pkgver}~Cleanjaro|g" "configure.ac"

	echo "Pull in latest language files..."
	./linguas.sh

	echo "Remove not working langs which need LC_ALL=C.UTF-8..."
	sed -e 's#en@cyrillic en@greek##g' -i "po/LINGUAS"

	echo "Avoid problem with unifont during compile of grub..."
	# http://savannah.gnu.org/bugs/?40330 and https://bugs.archlinux.org/task/37847
	gzip -cd "${srcdir}/unifont-${_UNIFONT_VER}.bdf.gz" > "unifont.bdf"

	echo "Run bootstrap..."
	./bootstrap \
		--gnulib-srcdir="${srcdir}/gnulib/" \
		--no-git
}

_build_grub-common_and_bios() {
	echo "Set ARCH dependent variables for bios build..."
	if [[ "${CARCH}" == 'x86_64' ]]; then
		_EFIEMU="--enable-efiemu"
	else
		_EFIEMU="--disable-efiemu"
	fi

	echo "Copy the source for building the bios part..."
	cp -r "${srcdir}/grub/" "${srcdir}/grub-bios/"
	cd "${srcdir}/grub-bios/"

	echo "Add the grub-extra sources for bios build..."
	install -d "${srcdir}/grub-bios/grub-extras"
	cp -r "${srcdir}/grub-extras/915resolution" \
		"${srcdir}/grub-bios/grub-extras/915resolution"
	export GRUB_CONTRIB="${srcdir}/grub-bios/grub-extras/"

	echo "Unset all compiler FLAGS for bios build..."
	unset CFLAGS
	unset CPPFLAGS
	unset CXXFLAGS
	unset LDFLAGS
	unset MAKEFLAGS

	echo "Run ./configure for bios build..."
	./configure \
		--with-platform="pc" \
		--target="i386" \
		"${_EFIEMU}" \
		--enable-boot-time \
		"${_configure_options[@]}"

	echo "Run make for bios build..."
	make
}

_build_grub-efi() {
	echo "Copy the source for building the ${_EFI_ARCH} efi part..."
	cp -r "${srcdir}/grub/" "${srcdir}/grub-efi-${_EFI_ARCH}/"
	cd "${srcdir}/grub-efi-${_EFI_ARCH}/"

	echo "Unset all compiler FLAGS for ${_EFI_ARCH} efi build..."
	unset CFLAGS
	unset CPPFLAGS
	unset CXXFLAGS
	unset LDFLAGS
	unset MAKEFLAGS

	echo "Run ./configure for ${_EFI_ARCH} efi build..."
	./configure \
		--with-platform="efi" \
		--target="${_EFI_ARCH}" \
		--disable-efiemu \
		--enable-boot-time \
		"${_configure_options[@]}"

	echo "Run make for ${_EFI_ARCH} efi build..."
	make
}

_build_grub-emu() {
	echo "Copy the source for building the emu part..."
	cp -r "${srcdir}/grub/" "${srcdir}/grub-emu/"
	cd "${srcdir}/grub-emu/"

	echo "Unset all compiler FLAGS for emu build..."
	unset CFLAGS
	unset CPPFLAGS
	unset CXXFLAGS
	unset LDFLAGS
	unset MAKEFLAGS

	echo "Run ./configure for emu build..."
	./configure \
		--with-platform="emu" \
		--target="${_EMU_ARCH}" \
		--enable-grub-emu-usb=no \
		--enable-grub-emu-sdl=no \
		--disable-grub-emu-pci \
		"${_configure_options[@]}"

	echo "Run make for emu build..."
	make
}

build() {
	cd "${srcdir}/grub/"

	echo "Build grub bios stuff..."
	_build_grub-common_and_bios

	echo "Build grub ${_EFI_ARCH} efi stuff..."
	_build_grub-efi

	if [[ "${CARCH}" == "x86_64" ]] && [[ "${_IA32_EFI_IN_ARCH_X64}" == "1" ]]; then
		echo "Build grub i386 efi stuff..."
		_EFI_ARCH="i386" _build_grub-efi
	fi

	if [[ "${_GRUB_EMU_BUILD}" == "1" ]]; then
		echo "Build grub emu stuff..."
		_build_grub-emu
	fi
}

_package_grub-common_and_bios() {
	cd "${srcdir}/grub-bios/"

	echo "Run make install for bios build..."
	make DESTDIR="${pkgdir}/" bashcompletiondir="/usr/share/bash-completion/completions" install

	echo "Remove gdb debugging related files for bios build..."
	rm -f "${pkgdir}/usr/lib/grub/i386-pc"/*.module || true
	rm -f "${pkgdir}/usr/lib/grub/i386-pc"/*.image || true
	rm -f "${pkgdir}/usr/lib/grub/i386-pc"/{kernel.exec,gdb_grub,gmodule.pl} || true

	echo "Install /etc/default/grub (used by grub-mkconfig)..."
	install -D -m0644 "${srcdir}/grub.default" "${pkgdir}/etc/default/grub"

	msg "Install grub.cfg for backup array"
	install -D -m0644 "${srcdir}/grub.cfg" "${pkgdir}/boot/grub/grub.cfg"

	msg "Install update-grub"
	install -Dm755 "${srcdir}/update-grub" "${pkgdir}/usr/bin/update-grub"

	msg "Install grub background"
	install -Dm644 "${srcdir}/background.png" "${pkgdir}/usr/share/grub/background.png"	
}

_package_grub-efi() {
	cd "${srcdir}/grub-efi-${_EFI_ARCH}/"

	echo "Run make install for ${_EFI_ARCH} efi build..."
	make DESTDIR="${pkgdir}/" bashcompletiondir="/usr/share/bash-completion/completions" install

	echo "Remove gdb debugging related files for ${_EFI_ARCH} efi build..."
	rm -f "${pkgdir}/usr/lib/grub/${_EFI_ARCH}-efi"/*.module || true
	rm -f "${pkgdir}/usr/lib/grub/${_EFI_ARCH}-efi"/*.image || true
	rm -f "${pkgdir}/usr/lib/grub/${_EFI_ARCH}-efi"/{kernel.exec,gdb_grub,gmodule.pl} || true
}

_package_grub-emu() {
	cd "${srcdir}/grub-emu/"

	echo "Run make install for emu build..."
	make DESTDIR="${pkgdir}/" bashcompletiondir="/usr/share/bash-completion/completions" install

	echo "Remove gdb debugging related files for emu build..."
	rm -f "${pkgdir}/usr/lib/grub/${_EMU_ARCH}-emu"/*.module || true
	rm -f "${pkgdir}/usr/lib/grub/${_EMU_ARCH}-emu"/*.image || true
	rm -f "${pkgdir}/usr/lib/grub/${_EMU_ARCH}-emu"/{kernel.exec,gdb_grub,gmodule.pl} || true
}

package() {
	cd "${srcdir}/grub/"

	echo "Package grub ${_EFI_ARCH} efi stuff..."
	_package_grub-efi

	if [[ "${CARCH}" == "x86_64" ]] && [[ "${_IA32_EFI_IN_ARCH_X64}" == "1" ]]; then
		echo "Package grub i386 efi stuff..."
		_EFI_ARCH="i386" _package_grub-efi
	fi

	if [[ "${_GRUB_EMU_BUILD}" == "1" ]]; then
		echo "Package grub emu stuff..."
		_package_grub-emu
	fi

	echo "Package grub bios stuff..."
	_package_grub-common_and_bios

	install -D -m644 "${srcdir}/${pkgname}.hook" "${pkgdir}/usr/share/libalpm/hooks/99-${pkgname}.hook"
}
