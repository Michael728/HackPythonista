# Linux双向ssh免密登录

## 原理

双向，顾名思义，双方互通，此处的意思是多台 linux 两两免密登录。双向比单向多了些操作，单向只需把某一个linux的公钥发送给其他linux即可，而双向要实现集群中的每一台机器都保存其他所有机器的公钥。

## 步骤

假设，你有两台机器，`ip`分别为`A`和`B`：

总共分为三步：
1. 生成公钥
2. 将A机器的公钥拷贝至B机器
3. 将B机器的公钥拷贝至A机器

### 生成公钥

如下命令生成公钥，默认会在`~/.ssh/`下生成`id_rsa`和`id_rsa.pub`。先检查一下机器是否已有公钥，如果没有再执行：

```
ssh-keygen -t rsa
```

-t 指定算法
-f 指定生成秘钥路径
-N 指定密码

### 拷贝公钥

```
cd ~/.ssh
scp id_rsa.pub root@B:/root/.ssh/authorized_keys #此命令在A机器执行，目的将公钥发送至B机器
scp id_rsa.pub root@A:/root/.ssh/authorized_keys #此命令在B机器执行，目的将公钥发送至B机器
```
scp: 加密的方式在本地主机和远程主机之间复制文件

参数:
- 源文件：指定要复制的源文件。也可以是远程地址
- 目标文件：目标文件。格式为`user@host：filename（文件名为目标文件的名称）`。

### 验证

```
ssh B #在A机器上，看是否免密登陆B
ssh A #在A机器上，看是否免密登陆B
```

如果发现设置免密登陆，还需要输入密码，那么检查一下`/root``.ssh``authorized_keys`目录和文件的权限。

```
chmod 600 authorized_keys
chmod 700 .ssh
```

> 如果authorized_keys文件、$HOME/.ssh目录 或 $HOME目录让本用户之外的用户有写权限，那么sshd都会拒绝使用 ~/.ssh/authorized_keys 文件中的key来进行认证的。

## 参考

- [Linux互通SSH免密码访问](https://blog.csdn.net/xiaowanziwuha/article/details/47265017)
- [服务器免密登录的实现以及异常解决方案](https://blog.csdn.net/simongeek/article/details/53501629)
- [Linux 双向 SSH 免密登录](http://zhoupq.com/Linux-%E5%8F%8C%E5%90%91-SSH-%E5%85%8D%E5%AF%86%E7%99%BB%E5%BD%95/)
- [Centos SSH 免密码互通](https://blog.csdn.net/tyfunwang/article/details/50338729)
- [scp命令](https://github.com/jaywcjlove/linux-command/blob/master/command/scp.md)