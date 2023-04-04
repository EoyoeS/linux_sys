先在 ==/boot==下添加所需的new_initramfs.img
```bash
vi /etc/grub.d/40_custom
```

```sh
#!/bin/sh
exec tail -n +3 $0

# This file provides an easy way to add custom menu entries.  Simply type the
# menu entries you want to add after this comment.  Be careful not to change
# the 'exec tail' line above.
menuentry "New Initramfs" {
    set root=(hd0,1)
    linux16 /vmlinuz-3.10.0-1160.el7.x86_64 root=/dev/mapper/centos-root ro crashkernel=auto rd.lvm.lv=centos/root rd.lvm.lv=centos/swap rhgb quiet
    initrd16 /new_initramfs.img
}
```

更新，重新生成grub.cfg
```bash
grub2-mkconfig -o /boot/grub2/grub.cfg
```