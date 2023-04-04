用当前目录
```bash
find . | cpio -c -o | gzip -9 > /boot/new_initramfs.img
```
后续[[在grub启动配置文件中增加入口]]