# Common Command Line and Script in Linux

* CPU相关操作
```
top  # 查看内存及CPU使用情况
htop  # 查看内存及CPU使用更详细情况, sudo apt-get install htop
free -m  # 单独查看内存使用情况
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
