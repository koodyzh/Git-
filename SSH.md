## 配置SSH
为实现本地和远程仓库之间免密钥登录，需要配置SSH

### 配置SSH，先在本地配置，再发送给远程

1. 在本地生成SSH
运行以下命令：
> $ ssh-keygen -t rsa -C koodyzh@icloud.com

2.发送给远程
> github ->settings ->SSH and ... -> New SSH  

将本地刚生成的id_rsa.pub中的内容复制到远程的key中

### 测试连通性
运行如下命令：
> $ ssh -T git@github.com

### 成功
如果本地和远程通信成功，则可以在本地/.ssh目录中发现 known_hosts文件

