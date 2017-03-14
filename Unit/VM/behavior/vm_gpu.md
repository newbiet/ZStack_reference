# 设置云主机显卡


### 场景描述

1.用户设置云主机显卡类型为cirrus时，使用 `ps -ef | grep qemu`查看‘-device’后的显示类型为`-device cirrus-vga`。该选项改变后， 只针对新创建的云主机和停止后再启动的云主机生效。提供一种简单的显卡类型，但对某些操作系统，无法提供更好的显示支持。(admin)

2.用户设置云主机显卡类型为vga时，使用 `ps -ef | grep qemu`查看‘-device’后的显示类型为`-device VGA`.该选项改变后， 只针对新创建的云主机和停止后再启动的云主机生效。vga是一种提供更好分辨率的显卡类型。(admin)

3.用户设置云主机显卡类型为vga时，使用 `ps -ef | grep qemu`查看‘-device’后的显示类型为`-device qxl-vga`。该选项改变后， 只针对新创建的云主机和停止后再启动的云主机生效。qxl显卡类型可以让VNC或SPICE协议有更好的性能。(admin)

