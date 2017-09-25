## Vim使用
i：在当前字符的左边插入  
I：在当前行首插入  
a：在当前字符的右边插入  
A：在当前行尾插入  
o：在当前行下面插入一个新行  
O：在当前行上面插入一个新  
h: 向前移动一个字符  
j: 向上移动一行  
k: 向下移动一行  
l: 向后移动一个字符  
yy: 复制当前一行  
dd:剪切当前一行  
p: 粘贴内容到游标之后  
P: 粘贴内容到游标之前  
## 文件　

    vim file  /  touch file 创建文件  
    cp file file1 复制  
    cp file  /home/linux/file1 复制到..  
    cat file 查看  
    mv file /home/linux/  移动
    mv file file2　重命名
## 目录

    mkdir dir　创建目录
    cp dir   dir1  -a　复制
    cp dir   /home/linux/dir2  -a　复制到..
    mv dir  dir2　重命名
    mv dir  /home/linux/　移动
    rm  dir  -rf　删除
    ls -d  dir　查看
    find  ./dir  -name  "filename"　查看
## 文件压缩归档
压缩方式：

    gzip filename
    bzip2 filename
    gunzip filename
    bunzip2 filename
    
tar 文件解压:
    
    tar xvf file.tar.xz

## 在线与本地包管理
本地：

    安装
    dpkg -i xxx.deb    
    卸载    
    dpkg -r xxx
    卸载，移除所有配置文件
    dpkg -P xxx
    安装状态
    dpkg -s xxx
    安装路径查看
    dpkg -L xxx
在线：
    
    更新软件源
    apt-get update
    安装
    apt-get install xxx
    卸载
    apt-get remove xxx
    彻底卸载
    apt-get remove -purge xxx
    软件包源码下载
    apt-get source xxx
    二进制软件包下载
    apt-get download xxx 
    软件包信息查看
    apt-cache show xxx
    升级软件包
    apt-get upgrade
    软件包安装状态
    apt-cache policy xxx
    
    
## 文本传输服务器TFTP
是TCP/IP协议族中的一个用来在客户机与服务器之间进行简单文件传输的协议，提供不复杂、开销不大的文件传输服务，端口号为69。只可以完成上传和下载文件的功能。

１．检查

    dpkg -s tftpd-hpa
    dpkg -s tftp-hpa
2.安装

    sudo apt-get update
    sudo apt-get install tftpd-hpa
    sudo apt-get install tftp-hpa
    如果有依赖
    sudo apt-get install -f
3.配置
    
    cd /etc/default/tftpd-hpa
    
    TFTP_USERNAME="tftp"
    TFTP_DIRECTORY="/var/lib/tftpboot"
    TFTP_ADDRESS="[::]:69"
    TFTP_OPTIONS="--secure  -c -l"
4.操作

    需要足够的权限操作
    启动
    service tftpd-hpa start
    重启
    service tftpd-hpa start
    停止
    service tftpd-hpa stop
    
5.使用

    链接后的操作
    链接服务器
    tftp IP
    上传文件
    put putfile
    下载文件
    get getfile
    退出
    quit
## NFS服务器安装
它允许网络中的计算机之间通过TCP/IP网络共享资源。在NFS的应用中，本地NFS的客户端应用可以透明地读写位于远端NFS服务器上的文件，就像访问本地文件一样。
1.检查

    dpkg -s nfs-kernel-server
2.安装
    
    sudo apt-get update
    sudo apt-get install nfs-kernel-server
3.NFS服务器配置

    cd /etc/exports
 
    # /etc/exports: the access control list for filesystems which may be exported
    #     to NFS clients.  See exports(5).
    #
    # Example for NFSv2 and NFSv3:
    # /srv/homes  hostname1(rw,sync,no_subtree_check) hostname2(ro,sync,no_subtree_check)
    #
    # Example for NFSv4:
    # /srv/nfs4        gss/krb5i(rw,sync,fsid=0,crossmnt,no_subtree_check)
    # /srv/nfs4/homes  gss/krb5i(rw,sync,no_subtree_check)
    #
    比如可以设置为  /nfs_root_dir  *(rw,sync,no_subtree_check,no_root_squash)
4.操作

    启动
    service nfs-kernel-server start
    重启
    service nfs-kernel-server restart
    停止
    service nfs-kernel-server stop
5.使用

    创建挂载
    mkdir /mount_nfs
    客户端挂载远端NFS服务器
    mount -t nfs IP:/nfs_root_dir /mount_nfs
    挂载成功后操作本地的mount_nfs目录就相当于操作远端的nfs_root_dir目录了
    
