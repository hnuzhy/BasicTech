# Common Command Line and Script in Linux

* 系统相关
```
uname -a  # 查看当前操作系统内核信息
sudo dmidecode | grep "Product Name"  # 查看机器型号
sudo dmidecode |grep -A16 "Memory Device$"|grep Size  # 查看机器有几个内存插槽及已使用几个
```

* 网卡
```
dmesg | grep -i eth  # 查看网卡信息
lspci |egrep -i eth  # 查看有几块网卡
```

* CPU相关操作
```
top  # 查看内存及CPU使用情况
htop  # 查看内存及CPU使用更详细情况, sudo apt-get install htop
free -m  # 单独查看内存使用情况
cat /proc/cpuinfo | grep name | cut -f2 -d: | uniq -c  # 查看CPU基本信息（逻辑CPU、型号、频率等）
cat /proc/cpuinfo | grep physical | uniq -c  # 查看CPU实际的物理核数
cat /proc/meminfo  # 查看内存详细信息
```

* GPU相关操作
```
nvidia-smi  # 查看GPU占用情况
watch -n 3 nvidia-smi  # 每隔n秒显示刷新一次GPU详情
```

* 文件解压缩
```
tar -xvf file.tar  # 解压tar
tar -xzvf file.tar.gz  # 解压tar.gz
tar -xjvf file.tar.bz2  # 解压 tar.bz2
```

* 文件复制
```
cp -r /folder/source /folder/target   # 文件夹使用-r --recursive
```

* 文件大小
```
du -sh *  # 显示文件夹下所有文件大小
df -h  # 显示机器上整个文件系统的使用情况
```
