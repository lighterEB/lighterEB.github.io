## 1.创建交换空间目录

```shell
cd /usr/
mkdir swap
dd if=/dev/zero of=swapfile bs=100M count=50
```

这条命令从硬盘里分出一个100M ×50 = 5G 大小的空间，挂在swapfile上

`注意`：这里我们bs(buff size)给的100M, bs大小可以根据free -h命令查看的buff/cache的大小来决定，如果给大了可能会报dd: memory exhausted by input buffer of size 1073741824 bytes (1.0 GiB) 

## 2.修改交换空间目录权限

```shell
chmod -R 0600 /usr/swap
```

## 3.创建交换分区文件

```shell
mkswap /usr/swap/swapfile
```

## 4.激活交换分区文件

```shell
swapon /usr/swap/swapfile
```

## 5.配置开机自动挂载

为了避免重启失效，需要配置开机自动激活交换分区文件

编辑`/etc/fstab`

```shell
vim /etc/fstab
```

在文件中增加一行

```shell
/usr/swap/swapfile swap swap defaults 0 0
```

保存退出

```shell
:wq
```
