================
How to build bsp
================

1. Install dependencies
=======================

-   on Fedora
.. highlights::

   .. code:: sh
      $ sudo dnf install autoconf automake curl python3 libmpc-devel mpfr-devel gmp-devel gawk bison flex texinfo gperf libtool patchutils bc openssl dkms libudev-devel golang-bin zlib-devel  qemu-user-binfmt  qemu-user-static ncurses-devel expat-devel elfutils-libelf-devel pciutils-devel openssl-devel binutils-devel qemu-system-riscv-core
      $ sudo dnf groupinstall "Development Tools" "C Development Tools and Libraries"

-   on Ubuntu
.. highlights::

   .. code:: sh
      $ sudo apt-get install autoconf automake autotools-dev curl python3 libmpc-dev libmpfr-dev libgmp-dev gawk build-essential bison flex texinfo gperf libtool patchutils bc zlib1g-dev libexpat-dev libncurses-dev openssl libiberty-dev libssl-dev dkms libelf-dev libudev-dev libpci-dev golang-go qemu-user-binfmt qemu-system-misc  qemu-user-static

To build uroot, you need to install **go 1.17**, refer to https://tecadmin.net/how-to-install-go-on-ubuntu-20-04/. You can use the following reference to check the go version.


.. highlights::

   .. code:: sh

      $ go version

      go version go1.17 linux/amd64

2. Build from source
====================
-   Download source code

.. highlights::

   .. code:: sh

      $ git clone https://github.com/sophgo/bootloader-riscv.git
      $ git clone https://github.com/sophgo/linux-sophgo.git

- Build Cross toolchain for bsp

  Enter the bsp directory which is the same level as ``bootloader-riscv`` and
  ``linux-sophgo``, and build Cross toolchain by the following command:
  .. highlights::

   .. code:: sh
      $ CHIP=mango
      $ source bootloader-riscv/scripts/envsetup.sh
      $ build_rv_gcc

  You will get the following folders:

.. highlights::

   .. code::

      .
      ├── bootloader-riscv
      ├── linux-sophgo
      └── gcc-riscv
               ├── gcc-riscv64-unknown-elf
               └── gcc-riscv64-unknown-linux-gnu

-  Build

.. highlights::

   .. code:: sh

      $ CHIP=mango
      $ source bootloader-riscv/scripts/envsetup.sh
      $ build_rv_all

-   The output files are in the ``install/soc_mango/riscv64`` directory

   .. code:: sh

      .
      ├── bsp-debs
      │        ├── linux-headers-5.19.17+.deb
      │        ├── linux-image-5.19.17+-dbg.deb
      │        └── linux-image-5.19.17+.deb
      ├── fw_jump.bin
      ├── fw_jump.elf
      ├── initrd.img
      ├── mango.dtb
      ├── mango_evb_v0.1.dtb
      ├── mango_multi_chips.dtb
      ├── mango_multi_chips_pld.dtb
      ├── mango_pld.dtb
      ├── riscv64_Image
      ├── rootfs.cpio
      ├── sd.img
      ├── vmlinux
      └── zsbl.bin
