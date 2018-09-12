# LVM分区

盘面上可以细分出扇区（Sector）与柱面（Cylinder)两种单位，其中扇区每个为512bytes那么大。

通常所说的”硬盘分区”就是指修改磁盘分区表，它定义了”第n个磁盘块是从第 x个柱面到第y个柱面”.因此，当系统要读取第n个磁盘块时，就是去读硬盘上第x个柱面到第y个柱面的信息.

整块磁盘的第一个扇区特别重要，因为它记录了整块磁盘的重要信息：
1. 主引导分区（Master Boot Record, MBR）：可以安装引导加载程序的地方，有446bytes.
2. 分区表（partition table）：记录整块磁盘分区的状态，有64bytes。

## 磁盘分区表（partion table）
在分区表所在的64bytes容量中，总共分为四组记录区。每组记录区记录了该区段的起始与结束的柱面号码。

- 其实所谓的分区只是针对那个64bytes的分区表进行设置而已。
- 硬盘默认的分区表仅能写入四组分区信息
- 四组分区信息我们称为主（Primary）或者扩展（Extended）分区。
- 分区最小单位为柱面（cylinder）。

分区的优点：
1. 数据安全
2. 有助于数据读取的速度和性能

扩展分区的目的是使用额外的扇区记录分区信息，扩展分区本身并不能拿来格式化。由扩展分区切出来的分区，就被称为逻辑分区（logical partition）。逻辑分区的设备名称号码由5号开始。

主分区、扩展分区和逻辑分区的定义：
- 主分区与扩展分区最多可以有4个（磁盘限制）
- 扩展分区最多只有1个（操作系统限制）
- 逻辑分区是由扩展分区持续切割出来的分区
- 能够被格式化后作为数据访问的分区为主分区与逻辑分区，扩展分区无法格式化。
- 逻辑分区的个数依操作系统而不同，SATA硬盘则有11个逻辑分区（5号到15号）。

分区是个很麻烦的东西，因为它是以柱面为单位的“连续”磁盘空间，且扩展分区又是类似独立的磁盘空间。

扩展分区是不能直接用的，他是以逻辑分区的方式来使用的，所以说扩展分区可分成若干逻辑分区。 他们的关系是包含的关系，所有的逻辑分区都是扩展分区的一部分。


## 磁盘分区

#### LVM卷管理

```shell
disk=/dev/vdb
pvcreate ci-pv1 $disk # 磁盘还没有分主分区或者扩展分区，就可以直接创建物理卷了
lvcreate -L 100G  -n apkg ci-vg1 # or lvcreate -L 100G  --name apkg ci-vg1
lvdisplay #查看逻辑卷路径
mkfs.ext3 /dev/ci-vg1/apkg # 格式化
mount /dev/ci-vg1/apkg /apkg # 挂载
df -Th # 查看
```

接着，为了开机自动挂载，执行：

```shell
echo "mount /dev/ci-vg1/apkg /apkg" >> /etc/rc.d/rc.local
```

### 分区常用命令

- lsblk：查看磁盘分区情况 ★★★
- vgdisplay: 查看卷组信息
- vgs： 查看卷组信息，简略
- fdisk -l：查看系统内分区信息

## 参考

- [Linx卷管理详解](https://blog.csdn.net/wuweilong/article/details/7565530)
- [Linux逻辑卷详解总结](http://blog.chinaunix.net/uid-20696246-id-1892246.html)
- [Linux 磁盘和分区](https://gtcsq.readthedocs.io/en/latest/linux_tools/disk_note.html)
- [Linux LVM简明教程](https://linux.cn/article-3218-2.html)