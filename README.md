# espressobin-debian
minimal debian image for espressobin

## write image to disk
```
cd /mnt
cp debian-stretch-min-fs.tar.bz2 .
tar -xf debian-stretch-min-fs.tar.bz2
```

## U-boot settings
```
setenv image_name vmlinuz
setenv fdt_name boot/armada-3720.dtb
```
### mmc
```
setenv bootmmc 'mmc dev 0; ext4load mmc 0:1 $kernel_addr $image_name;ext4load mmc 0:1 $fdt_addr $fdt_name;setenv bootargs $console root=/dev/mmcblk0p1 initrd=initrd.img rw rootwait; booti $kernel_addr - $fdt_addr'
```
### usb:
```
setenv bootusb 'usb start;ext4load usb 0:1 $kernel_addr $image_name;ext4load usb 0:1 $fdt_addr $fdt_name;setenv bootargs $console root=/dev/sda1 initrd=initrd.img rw rootwait; booti $kernel_addr - $fdt_addr'
``` 
### boot:
```
setenv bootcmd 'mmc dev 0; ext4load mmc 0:1 $kernel_addr $image_name;ext4load mmc 0:1 $fdt_addr $fdt_name;setenv bootargs $console root=/dev/mmcblk0p1 initrd=initrd.img rw rootwait; booti $kernel_addr - $fdt_addr'
```
### store settings:
```
saveenv

reset
```
