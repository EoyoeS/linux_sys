initramfs由两部分组成
前面部分是cpio
后面部分是gzip压缩后的cpio
1. 先解压cpio部分
	```bash
	cpio -ivF /boot/initramfs-3.10.0-1160.el7.x86_64.img
	```
	输出：
	```
	.
	kernel
	kernel/x86
	kernel/x86/microcode
	kernel/x86/microcode/GenuineIntel.bin
	early_cpio
	204 blocks
	```
2. 再解压gzip
	可以看到前面cpio是204blocks，使用dd跳过，分离出来
	```bash
	dd if=/boot/initramfs-3.10.0-1160.el7.x86_64.img of=initramfs.img skip=204
	```
	再
	```bash
	zcat initramfs.img | cpio -idmv
	```
后续[[2_制作initramfs]]