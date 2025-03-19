# SOS_FPGA

Running on Zybo Z7  10.

# Downloading Petalinux



[2022.1 Download link: petalinux-v2022.1-04191534-installer.run](https://www.xilinx.com/member/forms/download/xef.html?filename=petalinux-v2022.1-04191534-installer.run "Vivado Petalinux 2022.1")

[Download page if link does not work](https://www.xilinx.com/support/download/index.html/content/xilinx/en/downloadNav/embedded-design-tools/archive.html "Vivado Petalinux download Archive")

Needed dependencies:
```bash
sudo apt install gawk gcc net-tools xterm autoconf libtool texinfo zlib1g-dev gcc-multilib build-essential zlib1g libncurses-dev zlib1g:i386 libtinfo5
```

Install petalinux:
```bash
chmod +x petalinux-v2022.1-04191534-installer.run
./petalinux-v2022.1-04191534-installer.run --dir ~/petalinux
```


# Rebuilding Petalinux with new bitstream

Getting Hardware Description from .xsa file
```bash
petalinux-config --get-hw-description ~/.xsa
```

Cleaning FSBL cache for new bitstream
```bash
petalinux-build -c fsbl-firmware -x cleanall
```

Fresh build to generate new zynq_fsbl
```bash
petalinux-build
```

Making new BOOT.BIN
```bash
petalinux-package --boot --format BIN --fsbl images/linux/zynq_fsbl.elf --u-boot--fpga images/linux/system.bit --dtb images/linux/system.dtb -o BOOT.BIN
```

### Now transfer BOOT.BIN and uImage to BOOT partition on SD-card.