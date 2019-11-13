# Nano u-boot

## 配置LCD

参考官方文档，进行配置。LCD

```
git clone https://github.com/hnhkj/u-boot.git
cd u-boot
git checkout nano-v2018.01-huang

make ARCH=arm CROSS_COMPILE=arm-linux-gnueabi- licheepi_nano_spiflash_defconfig
make ARCH=arm menuconfig

x:800,y:480,depth:18,pclk_khz:33000,le:87,ri:40,up:31,lo:13,hs:1,vs:1,sync:3,vmode:0
x:480,y:272,depth:18,pclk_khz:10000,le:42,ri:8,up:11,lo:4,hs:1,vs:1,sync:3,vmode:0
(PE6) LCD panel backlight pwm pin
[ ] LCD Panel backlight pwm is inverted.

[*] Enable boot arguments
(console=ttyS0,115200 panic=5 rootwait root=/dev/mtdblock3 rw rootfstype=jffs2)

[*] Enable a default value for bootcmd
bootcmd value
(sf probe 0 50000000; sf read 0x80c00000 0x100000 0x4000; sf read 0x80008000 0x110000 0x400000; bootz 0x80008000 - 0x80c00000)


make ARCH=arm CROSS_COMPILE=arm-linux-gnueabi- -j4
sunxi-fel -p spiflash-write 0 ./u-boot-sunxi-with-spl.bin

```
