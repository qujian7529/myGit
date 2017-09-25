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
    
## SSH服务器
SSH 为建立在应用层和传输层基础上的安全协议。SSH 是目前较可靠，专为远程登录会话和其他网络服务提供安全性的协议。利用 SSH 协议可以有效防止远程管理过程中的信息泄露问题。SSH最初是UNIX系统上的一个程序，后来又迅速扩展到其他操作平台。SSH在正确使用时可弥补网络中的漏洞。SSH客户端适用于多种平台。几乎所有UNIX平台—包括HP-UX、Linux、AIX、Solaris、Digital UNIX、Irix，以及其他平台，都可运行SSH。
1.检查

    dpkg -s openssh-server
    dpkg -s openssh-client

2.安装

    sudo apt-get update
    sudo apt-get install openssh-server
    sudo apt-get install openssh-client
3.配置
    
    /etc/ssh/sshd_config
    
    展示其中一个片段：
    # Package generated configuration file
    # See the sshd_config(5) manpage for details
    # What ports, IPs and protocols we listen for
    Port 22
    # Use these options to restrict which interfaces/protocols sshd will bind to
    #ListenAddress ::
    #ListenAddress 0.0.0.0
    Protocol 2
    # HostKeys for protocol version 2
    HostKey /etc/ssh/ssh_host_rsa_key
    HostKey /etc/ssh/ssh_host_dsa_key
    HostKey /etc/ssh/ssh_host_ecdsa_key
    HostKey /etc/ssh/ssh_host_ed25519_key
    #Privilege Separation is turned on for security
    UsePrivilegeSeparation yes

    # Lifetime and size of ephemeral version 1 server key
    KeyRegenerationInterval 3600
    ServerKeyBits 1024

    # Logging
    SyslogFacility AUTH
    LogLevel INFO

    # Authentication:
    LoginGraceTime 120
    PermitRootLogin without-password
    StrictModes yes

    RSAAuthentication yes
    PubkeyAuthentication yes
    #AuthorizedKeysFile %h/.ssh/authorized_keys

    # Don't read the user's ~/.rhosts and ~/.shosts files
    IgnoreRhosts yes
    # For this to work you will also need host keys in /etc/ssh_known_hosts
    RhostsRSAAuthentication no
    # similar for protocol version 2
    HostbasedAuthentication no
    # Uncomment if you don't trust ~/.ssh/known_hosts for RhostsRSAAuthentication
    #IgnoreUserKnownHosts yes

    # To enable empty passwords, change to yes (NOT RECOMMENDED)
    PermitEmptyPasswords no

    # Change to yes to enable challenge-response passwords (beware issues with
    # some PAM modules and threads)
    ChallengeResponseAuthentication no

    # Change to no to disable tunnelled clear text passwords
    #PasswordAuthentication yes

    # Kerberos options
    #KerberosAuthentication no
    #KerberosGetAFSToken no
    #KerberosOrLocalPasswd yes
    #KerberosTicketCleanup yes

    # GSSAPI options
    #GSSAPIAuthentication no
    #GSSAPICleanupCredentials yes

    X11Forwarding yes
    X11DisplayOffset 10
    PrintMotd no
    PrintLastLog yes
    TCPKeepAlive yes
    #UseLogin no

    #MaxStartups 10:30:60
    #Banner /etc/issue.net

    # Allow client to pass locale environment variables
    AcceptEnv LANG LC_*

    Subsystem sftp /usr/lib/openssh/sftp-server
    port 设置sshd监听的端口号。
4.参数

    ListenAddress 设置sshd服务器绑定的IP地址
    HostKey 设置包含计算机私人密匙的文件
    ServerKeyBits 定义服务器密匙的位数
    LoginGraceTime 设置如果用户不能成功登录,在切断连接之前服务器需要等待的时间(以秒为单位)。
    KeyRegenerationInterval 设置在多少秒之后自动重新生成服务器的密匙(如果使用密匙)。重新生成密匙是为了防止用盗用的密匙解密被截获的信息。
    PermitRootLogin 设置 root 能不能用ssh登录。这个选项一定不要设成yes。
    X11Forwarding 设置是否允许 X11 转发
5.操作

    启动
    service ssh start
    重启
    service ssh restart
    停止
    service ssh stop
6.使用

    ssh linx@IP
    输入密码　既可以操作该ip电脑文件
