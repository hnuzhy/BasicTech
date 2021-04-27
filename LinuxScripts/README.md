# Common Command Line and Script in Linux

* 系统相关
```
Ctrl+Alt+F3  # Ubuntu开机过程中操作，进入命令行交互界面
uname -a  # 查看当前操作系统内核信息
sudo dmidecode | grep "Product Name"  # 查看机器型号
sudo dmidecode |grep -A16 "Memory Device$"|grep Size  # 查看机器有几个内存插槽及已使用几个
sudo adduser username -m  # 为系统添加新用户，默认添加后的用户主文件夹在/home下，-m可保证一定在/home目录下
sudo passwd username  # 为系统的新用户设置用户登陆密码，这一步骤紧跟添加新用户之后
su username  # 切换到某个用户账号下，需要输入该用户密码
sudo userdel -r username  # 删除某个用户，加上-r可以删除/home/路径下的用户文件夹，否则不能
sudo chown -R username:username /path/to/data/username  # 将某个目录下的访问权限绑定到某个用户
grep bash /etc/passwd  # 查看系统下所有存在的用户名（/home目录下不一定真实）
```

* 网卡
```
dmesg | grep -i eth  # 查看网卡信息
lspci |egrep -i eth  # 查看有几块网卡
ifconfig  # 查看网络配置信息
ifconfig eth0 down && ifconfig eth0 up  # 方法1，将网卡网络服务禁用或开启，eth0为网卡名
ifdown eth0 && ifup eth0  # 方法2，将网卡网络服务禁用或开启，eth0为网卡名，需已安装apt install ifupdown2
sudo vi /etc/network/interfaces  # 查看网卡信息，并为网卡配置静态IP地址，需要root用户；退出并保存("Esc"+":wq")
sudo service networking restart  # Linux中重新启动网卡网络服务，但Ubuntu下可能不可用
sudo service NetworkManager restart  # Ubuntu下重新启动网卡网络服务，使用ifconfig亦可
```

* 修改默认端口号
```
sudo vi /etc/ssh/sshd_config /etc/ssh/sshd_config.bak  # 备份一下相关系统配置文件
sudo vi /etc/ssh/sshd_config  # 修改系统配置文件，选择性注释掉“Port 22”，添加新的端口号“Port 2222”
iptables -A INPUT -p tcp --dport 2222 -j ACCEPT  # 添加到路由表，将修改内容执行生效
sudo /etc/init.d/sshd restart  # 重启sshd文件生效
sudo service ssh restart  # 如果上面的命令行不通，试一下这种方式重启sshd文件生效
netstat -an | grep "LISTEN "  # 查看端口状态
```

* 配置静态IP地址
```
sudo vi /etc/network/interfaces  # 只适用于系统版本低于Ubuntu18.04的Linux操作系统
sudo service NetworkManager restart

cd /etc/netplan & sudo vi 50-cloud-init.yaml  # 适用于系统版本为Ubuntu18.04的Linux操作系统
sduo netplan apply

netstat -rn  # 查看gateway4等配置是否正确
telnet 192.168.1.11 2222  # 测试新配置的对应的IP地址和端口号是否可正常的访问
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
cat /usr/local/cuda/version.txt  # 查看CUDA版本
cat /usr/local/cuda/include/cudnn.h | grep CUDNN_MAJOR -A 2  # 查看cudnn版本
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

# 远程从某台服务器上拷贝文件。-r针对文件夹；-v动态显示信息；如果该服务器端口不是默认的22，使用-P修改
scp -r -v -P 2345 username@server_IP:/folder/source /folder/target

# 远程同步服务器文件，比scp更强大，不修改文件创建日期，可以不覆盖式传输，支持断点传输。
# -e后的引号内表示修改端口号，-avzut表示的内容，请自行使用rsync -h查看。
# 关于大量文件（文件小而多，传输极为耗时）的远传，需要自行写多线程传输的逻辑代码。
rsync -avzut -e 'ssh -p 2345' username@hostname:SourceFile DestFile  
```

* 文件大小与个数
```
du -sh *  # 显示文件夹下所有文件大小
df -h  # 显示机器上整个文件系统的使用情况
du -B G --max-depth=1  # 以GB为单位显示深度为1的当前各文件夹下的所占存储大小
ls -l ./your/path/ | grep "-" | wc -l  # 查看某文件夹下文件的个数(不包含子文件)
ls -lR ./your/path/ | grep "-" | wc -l  # 查看某文件夹下文件的个数(包含子文件)
```
