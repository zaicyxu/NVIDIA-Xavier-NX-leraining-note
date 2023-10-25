# Jetson NX Plus SSD card

## 挂载ssd到系统

1. 安装M.2 SSD固态硬盘

将Jetson Xavier NX关机断开电源，M.2固态硬盘插座在底部。首先把固定的螺丝拧下来，然后按照下图方式，将固态硬盘的金手指插入硬盘插槽，安装好固态硬盘并拧紧螺丝。

![https://www.yahboom.com/Public/ueditor/php/upload/image/20210811/1628662679347473.png](https://www.yahboom.com/Public/ueditor/php/upload/image/20210811/1628662679347473.png)

然后撕下导热硅脂片的保护膜并贴到散热片上。

![https://www.yahboom.com/Public/ueditor/php/upload/image/20210811/1628662682400177.png](https://www.yahboom.com/Public/ueditor/php/upload/image/20210811/1628662682400177.png)

最后将散热片贴到固态硬盘上。

![https://www.yahboom.com/Public/ueditor/php/upload/image/20210811/1628662688131317.png](https://www.yahboom.com/Public/ueditor/php/upload/image/20210811/1628662688131317.png)

2.给Jetson Xavier NX上电开机，此时df -h检查硬盘信息可能无法识别到硬盘，所以需要对硬盘进行格式化并挂载到系统上。

![https://www.yahboom.com/Public/ueditor/php/upload/image/20210811/1628662698476470.png](https://www.yahboom.com/Public/ueditor/php/upload/image/20210811/1628662698476470.png)

3. 输入以下命令检查所有分区信息，向下翻可以找到/dev/nvme0n1有一个我们插入的m.2固态硬盘。

sudo fdisk -l

![https://www.yahboom.com/Public/ueditor/php/upload/image/20210811/1628662702282501.png](https://www.yahboom.com/Public/ueditor/php/upload/image/20210811/1628662702282501.png)

这里显示的119,2 GiB其实是119.2 GiB，只是小数点默认显示了逗号。

4.打开Jetson Xavier NX系统自带的磁盘分区工具Disks。

![https://www.yahboom.com/Public/ueditor/php/upload/image/20210811/1628662706369415.png](https://www.yahboom.com/Public/ueditor/php/upload/image/20210811/1628662706369415.png)

5.格式化硬盘

选择我们接入的M.2固态硬盘，这里注意不能选择错误，否则会造成系统奔溃。然后按快捷键‘Ctrl+F’或者打开右上角的三条横杠，选择Format Disk.

![https://www.yahboom.com/Public/ueditor/php/upload/image/20210811/1628662710560760.png](https://www.yahboom.com/Public/ueditor/php/upload/image/20210811/1628662710560760.png)

![https://www.yahboom.com/Public/ueditor/php/upload/image/20210811/1628662714294677.png](https://www.yahboom.com/Public/ueditor/php/upload/image/20210811/1628662714294677.png)

![https://www.yahboom.com/Public/ueditor/php/upload/image/20210811/1628662716329589.png](https://www.yahboom.com/Public/ueditor/php/upload/image/20210811/1628662716329589.png)

输入NX系统的密码并确认。

![https://www.yahboom.com/Public/ueditor/php/upload/image/20210811/1628662721373687.png](https://www.yahboom.com/Public/ueditor/php/upload/image/20210811/1628662721373687.png)

6. 新建磁盘分区

依然选择M.2固态硬盘，点击‘Create Disk Image’创建硬盘分区。这里我们要把SSD作为系统盘使用，所以直接将整个硬盘的空间作为一个分区就好。

![https://www.yahboom.com/Public/ueditor/php/upload/image/20210811/1628662724223083.png](https://www.yahboom.com/Public/ueditor/php/upload/image/20210811/1628662724223083.png)

填入磁盘名称，这里以SSD128为例，磁盘的格式必须选择Ext4。然后点击Create创建。

![https://www.yahboom.com/Public/ueditor/php/upload/image/20210811/1628662727604156.png](https://www.yahboom.com/Public/ueditor/php/upload/image/20210811/1628662727604156.png)

完成后如下图所示：

![https://www.yahboom.com/Public/ueditor/php/upload/image/20210811/1628662730101776.png](https://www.yahboom.com/Public/ueditor/php/upload/image/20210811/1628662730101776.png)

7. 挂载磁盘

点击拨号键，就可以看到已经挂载到系统上。同时拨号键会自动变成停止键。

![https://www.yahboom.com/Public/ueditor/php/upload/image/20210811/1628662734558563.png](https://www.yahboom.com/Public/ueditor/php/upload/image/20210811/1628662734558563.png)

再次在终端输入df -h就可以查到刚刚挂载的硬盘了。

![https://www.yahboom.com/Public/ueditor/php/upload/image/20210811/1628662736577789.png](https://www.yahboom.com/Public/ueditor/php/upload/image/20210811/1628662736577789.png)

**注意：第一步要和第二步连贯起来操作，因为第一步每一次重启后就会失效，所以如果中途关机，需要再次执行步骤一，再进行步骤二。**

## ****移动系统到固态硬盘****

注意：从JetPack4.6[REV.2]版本开始，增加了优先启动SSD系统的功能，所以系统刷入到SSD后，会自动从SSD启动，而不需要以下步骤。以下步骤只适合JetPack4.6以前的版本。

1. 安装rootOnNVME软件

打开NX的终端，在用户目录下输入以下代码

```jsx
git clone https://github.com/jetsonhacks/rootOnNVMe.git
```

进入rootOnNVME目录并查看文件

```jsx
cd rootOnNVMe/
```

```jsx
ls
```

![https://www.yahboom.com/Public/ueditor/php/upload/image/20210811/1628662881432647.png](https://www.yahboom.com/Public/ueditor/php/upload/image/20210811/1628662881432647.png)

2. 复制系统文件

输入以下命令复制文件到M.2固态硬盘。

```jsx
./copy-rootfs-ssd.sh
```

![https://www.yahboom.com/Public/ueditor/php/upload/image/20210811/1628662885253875.png](https://www.yahboom.com/Public/ueditor/php/upload/image/20210811/1628662885253875.png)

3.启动服务，运行后输入NX的密码，按回车键确认，看到以下信息就表示系统成功移动到M.2固态硬盘。

```jsx
./setup-service.sh
```

![https://www.yahboom.com/Public/ueditor/php/upload/image/20210811/1628662887946105.png](https://www.yahboom.com/Public/ueditor/php/upload/image/20210811/1628662887946105.png)

4.重启NX系统。

```jsx
sudo reboot
```

![https://www.yahboom.com/Public/ueditor/php/upload/image/20210811/1628662891324432.png](https://www.yahboom.com/Public/ueditor/php/upload/image/20210811/1628662891324432.png)

5. 打开NX的终端，输入以下命令查看储存空间。

```jsx
df -h
```

![https://www.yahboom.com/Public/ueditor/php/upload/image/20210811/1628662895992492.png](https://www.yahboom.com/Public/ueditor/php/upload/image/20210811/1628662895992492.png)

可以看到M.2固态硬盘开机会自动挂载在根目录上。打开文件管理器也能够看到系统空间变大了。

![https://www.yahboom.com/Public/ueditor/php/upload/image/20210811/1628662897270385.png](https://www.yahboom.com/Public/ueditor/php/upload/image/20210811/1628662897270385.png)